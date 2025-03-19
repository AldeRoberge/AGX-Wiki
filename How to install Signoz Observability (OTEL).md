https://signoz.io/docs/install/docker/




0. Login into the VPS : 

```bash
ssh root@IP_ADDRESS
```

1. In a directory of your choosing, clone the SigNoz repository and 'cd' into the `signoz/deploy` directory by entering the following commands:

```bash
git clone -b main https://github.com/SigNoz/signoz.git && cd signoz/deploy/
```

2. Run the `install.sh` script:

```batch
cd deploy 

./install.sh
```

Be very patient, it can take a long time.