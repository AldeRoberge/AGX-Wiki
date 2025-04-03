---
tags:
  - daily
  - hours
  - time
  - graph
  - pie-chart
  - statistics
  - lifestyle
---

![[Daily_Schedule.png]]


```python
import matplotlib.pyplot as plt
import numpy as np

def time_to_hours(time_str, start_hour=None):
    """
    Convert a time string "HH:MM" to a float representing hours.
    If the time is "00:00" and start_hour is provided and greater than 0,
    assume that it represents midnight at the end of the day (i.e., 24:00).
    """
    h, m = map(int, time_str.split(":"))
    hours = h + m/60
    if hours == 0 and start_hour is not None and start_hour > 0:
        hours = 24.0
    return hours

# Define the schedule with start and end times in "HH:MM" format
schedule_str = [
    ('Sleeping',   "00:00", "07:30"),
    ('Waking',     "07:30", "08:00"),
    ('Eating',     "08:00", "08:20"),
    ('Walking',    "08:20", "08:30"),
    ('Working',    "08:30", "12:00"),
    ('Walking',    "12:00", "12:10"),
    ('Eating',     "12:10", "12:50"),
    ('Walking',    "12:50", "13:00"),
    ('Working',    "13:00", "16:30"),
    ('Walking',    "16:30", "16:40"),
    ('Cooking',    "16:40", "18:15"),
    ('Eating',     "18:15", "19:00"),
    ('Cleaning',   "19:00", "20:00"),
    ('Relaxing',   "20:00", "22:00"),
    ('Sleeping',   "22:00", "00:00")
]

# Process the schedule to compute start times and durations (in hours)
processed_schedule = []
category_durations = {}

for activity, start_str, end_str in schedule_str:
    start = time_to_hours(start_str)
    end = time_to_hours(end_str, start_hour=start)
    if end < start:
        end += 24
    duration = end - start
    processed_schedule.append((activity, start, duration))

    # Aggregate durations by category
    if activity not in category_durations:
        category_durations[activity] = 0
    category_durations[activity] += duration

# Compute percentage of total time spent per category
total_time = sum(category_durations.values())
category_percentages = {activity: (duration / total_time) * 100 for activity, duration in category_durations.items()}

# Define more saturated colors for each unique activity:
color_map = {
    'Sleeping': '#34495E',   # Saturated Blue
    'Waking': '#FF6347',     # Tomato Red-Orange
    'Showering': '#00C1D4',  # Vivid Turquoise
    'Eating': '#2ECC71',     # Saturated Green
    'Walking': '#9B59B6',    # Rich Purple
    'Working': '#E74C3C',    # Bold Red
    'Relaxing': '#4A90E2',   # Deep Blue-Gray
    'Cooking': '#E67E22',    # Vivid Orange
    'Cleaning': '#16A085',   # Strong Teal
    'Playing': '#F1C40F'     # Bright Yellow
}

# Unpack the processed schedule into separate lists
activities = [item[0] for item in processed_schedule]
start_times = [item[1] for item in processed_schedule]
durations = [item[2] for item in processed_schedule]

# Convert times (in hours) into angles (radians)
start_angles = [(t / 24) * 2 * np.pi for t in start_times]
widths = [(d / 24) * 2 * np.pi for d in durations]

# Create the figure with a light background
fig, ax = plt.subplots(figsize=(8, 8), subplot_kw={'projection': 'polar'})
fig.patch.set_facecolor('#FDFDFD')  # Light background for the figure
ax.set_facecolor('#FDFDFD')         # Light background for the axes

# Remove grid lines (transversal lines)
ax.grid(False)

# Set the clock style: 00:00 (midnight) at the top and clock running clockwise.
ax.set_theta_zero_location('N')
ax.set_theta_direction(-1)

# Plot each segment using the defined saturated colors
for i in range(len(activities)):
    ax.bar(x=start_angles[i], height=1, width=widths[i],
           bottom=0, color=color_map[activities[i]], label=activities[i], align='edge')

# Remove duplicate labels in the legend
handles, labels = ax.get_legend_handles_labels()
unique = {}
for h, l in zip(handles, labels):
    if l not in unique:
        unique[l] = h

# Create legend labels with percentage
legend_labels = [f"{activity} ({category_percentages[activity]:.1f}%)" for activity in unique.keys()]

# Sort by percentage (descending order)
sorted_legend_labels = sorted(zip(legend_labels, unique.values()), key=lambda x: float(x[0].split('(')[1].split('%')[0]), reverse=True)

# Create the sorted legend
sorted_labels, sorted_handles = zip(*sorted_legend_labels)
legend = ax.legend(sorted_handles, sorted_labels, bbox_to_anchor=(1.05, 1), loc='upper left')

# Set legend background and text style for clarity on a light background
legend.get_frame().set_facecolor('#FDFDFD')
plt.setp(legend.get_texts(), color='black', fontweight='bold')

# Remove radial tick labels and ticks
ax.set_yticklabels([])
ax.set_yticks([])

# Define clock labels for every two hours along the outer circumference
ticks = [(h / 24) * 2 * np.pi for h in range(0, 24, 2)]
clock_labels = ['12 AM', '2 AM', '4 AM', '6 AM', '8 AM', '10 AM',
                '12 PM', '2 PM', '4 PM', '6 PM', '8 PM', '10 PM']
ax.set_xticks(ticks)
ax.set_xticklabels(clock_labels, color='black', fontsize=10, fontweight='bold')

# Set the title with dark text for contrast
plt.title("Daily Schedule", color='black', fontsize=14, fontweight='bold')

# Adjust tick parameters to use dark text
ax.tick_params(axis='x', colors='black')

plt.get_current_fig_manager().set_window_title('Daily Schedule')

plt.show()

```