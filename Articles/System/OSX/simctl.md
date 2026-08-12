# simctl

## Open

```bash
open /Applications/Xcode.app/Contents/Developer/Applications/Simulator.app/
```

## Listing all available simulators

```bash
xcrun simctl list
```


### Booted

```bash
xcrun simctl list | grep Booted
```


### DeviceType

```bash
xcrun simctl list | grep SimDeviceType
```

#### iPhone

```bash
xcrun simctl list | grep SimDeviceType.iPhone
```

#### iPad

```bash
xcrun simctl list | grep SimDeviceType.iPad
```

#### TV

```bash
xcrun simctl list | grep SimDeviceType.Apple-TV
```

#### Watch

```bash
xcrun simctl list | grep SimDeviceType.Apple-Watch
```



### Runtime

```bash
xcrun simctl list | grep SimRuntime
```


## CRUD operations on Simulators

### Create

```bash
xcrun simctl create iPhone\ X\ Custom com.apple.CoreSimulator.SimDeviceType.iPhone-X com.apple.CoreSimulator.SimRuntime.iOS-11-2
```

### Boot

```bash
xcrun simctl boot B69F849E-0E9C-41BB-A98B-B8255616886E
```

### Shutdown

```bash
xcrun simctl shutdown B69F849E-0E9C-41BB-A98B-B8255616886E
```

### Erase

```bash
xcrun simctl erase B69F849E-0E9C-41BB-A98B-B8255616886E
```

### Delete

```bash
xcrun simctl delete B69F849E-0E9C-41BB-A98B-B8255616886E
```
