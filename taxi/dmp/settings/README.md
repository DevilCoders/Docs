## HOW TO
Library retrieve configuration values.

**Features**:
- support different settings source
- merge multiple settings sources to single instance (allow split one huge file into small isolated files)

### Create settings instance

Settings instance for single yaml file:
```python
settings = build_settings("/path/to/settings.yaml")
```

Settings instance for multiple yaml files:
```python
settings = build_settings(
    "/path/to/low_priority_settings.yaml",
    "/path/to/high_priority_settings.yaml",
)
```

Settings instance for directory with yaml files:
```python
settings = build_settings("/path/to/settings_dir")
```

### Access to settings

Example yaml:
```yaml
a: hello world
b:
  b1: 100
  b2: 500
```

Settings instance return copy for collections. Returned collection could be changed on client side without affect state of settings instance.
```python
# keys as tuple
settigs(('b', 'b1'))  #return 100
# keys joined by dot
settings('b.b2')   #return 500
settings('b') #return dict(b1=100, b2=500)
```
