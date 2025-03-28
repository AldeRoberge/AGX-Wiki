Inspired by a post on Reddit by Pale-Relation-5735 titled ["Which C# Code Analyzers should I focus on"](https://www.reddit.com/r/dotnet/comments/1glzves/which_c_code_analyzers_should_i_focus_on/)

---

> Hey C#/.NET community!
> 
> I’m working on a C# project, and I want to improve code quality by adding some static code analyzers. After researching, I’ve narrowed it down to a few popular options:
> 
> - StyleCop.Analyzers: Mainly for enforcing code style and consistency.
> - SonarAnalyzer.CSharp: Known for its wide range of rules, including security and code quality.
> - Roslynator.Analyzers: Covers best practices and offers code fixes.
> - Meziantou.Analyzer: Focuses on performance, security, and .NET best practices.
> 
> My concern is that some of these analyzers may have overlapping rules, leading to redundancy and noise in the results. I’d love to hear your thoughts if you’ve worked with these! Specifically:
> 
> 1. Should I consider adding all four of them, or is there a more focused set that would cover most use cases effectively?
> 2. I’ve noticed a slight delay in build time since adding them but am not entirely sure they’re the cause. Has anyone else experienced build slowdowns with multiple analyzers, and if so, how did you handle it?
> 3. Have you noticed significant overlap among these analyzers, and if so, which ones tend to repeat rules?
> 4. Any tips for managing rule conflicts or disabling specific rules to reduce noise?
> 
> Thanks in advance for any advice!

---

The user asks a well formulated and interesting question that is applicable to my current situation. Here is a quick study of the available code analysers :

| Project      | StyleCop.Analyzers                                                   | SonarAnalyzer.CSharp                     | Roslynator.Analyzers                                                  | Meziantou.Analyzer                                      |
| ------------ | -------------------------------------------------------------------- | ---------------------------------------- | --------------------------------------------------------------------- | ------------------------------------------------------- |
| Last update  | 3 months ago                                                         | 6 hours ago                              | Last month                                                            | Last week                                               |
| Description  | An implementation of StyleCop rules using the .NET Compiler Platform | Code analyzer for C# and VB.NET projects | Roslynator is a set of code analysis tools for C#, powered by Roslyn. | A Roslyn analyzer to enforce some good practices in C#. |
| Commits      | 5200                                                                 | 7775                                     | 4378                                                                  | 821                                                     |
| Issues       | 390                                                                  | 529                                      | 176                                                                   | 2                                                       |
| Contributors | 103                                                                  | 82                                       | 43                                                                    | 27                                                      |

In the replies, one user points the OP to [a link](https://www.sqlite.org/testing.html#static_analysis) on SQLite's documentation that states that "More bugs have been introduced into SQLite while trying to get it to compile without warnings than have been found by static analysis.". While I admire SQLite, I think that since it's considerably lower level than C# (it's written in C), "static analysis" in this case might refer to something than static analysis in the context of C#.

Another user mentions that they use **Sonar** and **Roslynator**. 

I personally tried **StyleCop**, but found that it was outdated (provided **terrible suggestions** for new C# language features), and was very strict.

Another user jokingly points to [EvilRoslynAnalyzers](https://github.com/Aaronontheweb/EvilRoslynAnalyzers), which makes fun of strict code rules. This tool bans from using extension methods, and the var declaration 'like a 90s Java program'. 🤡

### Testing Analyzers

I added all analyzers, except for StyleCop, which I found very annoying.

```xml
      <PackageReference Include="Meziantou.Analyzer" Version="2.0.189">
	      ...
      <PackageReference Include="Roslynator.Analyzers" Version="4.13.1">
	      ...
      <PackageReference Include="SonarAnalyzer.CSharp" Version="10.7.0.110445">
	      ...
      ```

Looking through the newly analyzed code, there's a little bit of head scratching going on : 

For example : 

```csharp
public static readonly JsonSerializerSettings Settings = new()  
{  
    TypeNameHandling = TypeNameHandling.Auto,  
    Formatting = Formatting.Indented  
};
```

## My first encounter with **weird** rules

Generates the following warning : [MA0007 - Add a comma after the last value](https://github.com/meziantou/Meziantou.Analyzer/blob/main/docs/Rules/MA0007.md)

Which is .... Weird. I tried to find why would the analyzer be so opinionated about such things. 

For Javascript, Jeff B on StackOverflow mentions : 

1. Easier to add an item or re-order items. Before you always had to check the trailing comma and make sure it was present or removed depending on location.
2. Removes the need to have one line item be special because it lacks the `,`.
3. Allows for cleaner Git diffs.

[Same with Rust.](https://users.rust-lang.org/t/why-would-one-put-comma-after-the-last-field/14614)

Which is valid. But it also goes against the default JetBrains IntellIJ behavior of suggesting to remove the last comma.

## My first encounter with **stupid** rules

```csharp
public static async Task<Result<TResponse>> PostJson<TRequest, TResponse>(
```

Error : MA0051: Method is too long (64 lines; maximum allowed: 60)