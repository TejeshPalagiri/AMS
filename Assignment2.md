# Assignment2


```python
class Car:

    engine_status = False
    current_speed_engine = 0
    def __init__(self, color, max_speed, acceleration, tyre_friction):
        try:
            if(max_speed < 0):
                raise Exception
        
        except Exception:
            print("ValueError: Invalid value for max_speed  ")
        self.color = color
        self.max_speed = max_speed 
        self.acceleration = acceleration
        self.tyre_friction = tyre_friction
    def start_engine(self):
        self.engine_status = True

    @property
    def is_engine_stared(self):
        return self.engine_status

    
    def accelerate(self):
        if(self.engine_status):
            self.current_speed_engine += self.acceleration
        else:
            print("First start the engine to accelerate")


    def apply_brakes(self):
        if(self.current_speed_engine > 0):
            self.current_speed_engine -= self.tyre_friction
        
        else:
            print("The car stopped")


    def sound_horn(self):
        if(self.engine_status):
            print("Beep Beep")
        else:
            print('Start the engine to sound_horn')


    def stop_engine(self):
        if(self.engine_status):
            self.engine_status = False
        else:
            print("Already the car has been stopped")

    @property
    def current_speed(self):
        return "{}".format(self.current_speed_engine)
```


```python
class Truck(Car):
    
    cargo_weight = 0
    
    def __init__(self, color, max_speed, acceleration, tyre_friction, max_cargo_weight):
        super().__init__(color, max_speed, acceleration, tyre_friction)
        self.max_cargo_weight = max_cargo_weight
        
    def sound_horn(self):
        if(self.engine_status):
            print("Honk Honk")
        else:
            print('Start the engine to sound_horn')
            
    def load(self, weight):
        try:
            if(weight < 0):
                raise Exception
            else:
                if(int(self.current_speed) == 0):
                    if(self.max_cargo_weight >= weight and self.max_cargo_weight >= self.cargo_weight+weight):
                        self.cargo_weight += weight
                    else:
                        print('Cannot load cargo more than max limit:', self.max_cargo_weight)
                else:
                    print('Cannot load cargo during motion')
        except Exception:
            print("ValueError: Invalid value for cargo_weight")
        
    def unload(self, weight):
        try:
            if(weight < 0):
                raise Exception
            else:
                if(int(self.current_speed) == 0 ):
                    if(self.cargo_weight > 0 and self.max_cargo_weight >= weight and self.cargo_weight > 0 and self.cargo_weight - weight >= 0):
                        self.cargo_weight -= weight
                else:
                    print('Cannot un-load cargo during motion')
        except Exception:
            print("ValueError: Invalid value for cargo_weight")
```


```python
truck = Truck(color="Red", max_speed=250, acceleration=10, tyre_friction=3, max_cargo_weight=100)
```


```python
truck.load(50)
```


```python
truck.load(100)
```

    Cannot load cargo more than max limit: 100



```python
truck.load(-100)
```

    ValueError: Invalid value for cargo_weight



```python
truck = Truck(color="Red", max_speed=250, acceleration=10, tyre_friction=3, max_cargo_weight=100)  
```


```python
truck.start_engine()
```


```python
truck.accelerate() 
```


```python
truck.load(50)
```

    Cannot load cargo during motion



```python
truck.sound_horn()
```

    Honk Honk



```python
truck = Truck(color="Red", max_speed=250, acceleration=10, tyre_friction=3, max_cargo_weight=100)  
```


```python
truck.start_engine() 
```


```python
truck.load(50)
```


```python
truck.accelerate()  
```


```python
truck.unload(50)
```

    Cannot un-load cargo during motion



```python
truck.sound_horn()
```

    Honk Honk



```python
truck = Truck(color="Red", max_speed=250, acceleration=10, tyre_friction=3, max_cargo_weight=100)  
truck.start_engine() 
truck.load(50)
```


```python
truck.unload(80)
```


```python
truck.load(100)
```

    Cannot load cargo more than max limit: 100



```python
truck.unload(50)
```


```python
print(truck.cargo_weight)
```

    0



```python
truck.load(100)
```


```python
class RaceCar(Car):
    
    nitro_points = 0
    
    def sound_horn(self):
        if(self.engine_status):
            print("Peep Peep\nBeep Beep")
        else:
            print('Start the engine to sound_horn')
            
    def apply_brakes(self):
        if(int(self.current_speed) > 0):
            if(int(self.current_speed) > self.max_speed / 2):
                self.nitro_points += 10
            self.current_speed_engine -= self.tyre_friction
            
        else:
            print("The car stopped")
            
    def accelerate(self):
        if(self.engine_status):
            if(self.nitro_points):
                self.current_speed_engine += int(self.acceleration * 1.3)
                self.nitro_points -= 10
            else:
                self.current_speed_engine += self.acceleration
        else:
            print("First start the engine to accelerate")

```


```python
racecar = RaceCar(color="Red", max_speed=250, acceleration=50, tyre_friction=30)  
```


```python
racecar.start_engine() 
```


```python
racecar.accelerate()  
racecar.accelerate()  
racecar.accelerate() 
```


```python
print(racecar.current_speed  )
```

    150



```python
racecar.apply_brakes()
print(racecar.current_speed)
```

    120



```python
print(racecar.nitro_points)
```

    10



```python
racecar.accelerate()
```


```python
print(racecar.current_speed)
```

    185



```python
print(racecar.nitro_points)
```

    0



```python
racecar.accelerate()
```


```python
print(racecar.current_speed  )
```

    235



```python
racecar.apply_brakes()
racecar.apply_brakes()
racecar.apply_brakes()
print(racecar.current_speed)
```

    145



```python
print(racecar.nitro_points)
```

    30



```python
racecar.accelerate()
print(racecar.nitro_points)
```

    20



```python
print(racecar.current_speed)
```

    210



```python
racecar.accelerate()
racecar.accelerate()
print(racecar.nitro_points)
racecar.accelerate()
print(racecar.nitro_points)
```

    0
    0



```python
print(racecar.current_speed)
```

    390



```python

```
