# [fit] geobin.io
---

# Esri Portland R&D Center
__Courtland Fowler__
_@FowlerCourt_

__Josh Yaganeh__
_@hsoj_

__Ryan Arana__
_@aranasaurus_

__Nate Goldman__
_@ungoldman_

---

# [fit] It's like RequestBin
# [fit] + Geo

---

# [fit] Mini Demo

---

# [fit] Why did we make it?

---

# [fit] Demo!

### Geotrigger Editor __>__ Faker __>__ Geobin

---

# [fit] Components

- Parsing Data
- Websockets
- Rate-limiting Middleware
- Mocking Redis for tests
- Build/deployment Process

---

# [fit] Parsing the Data

---

# GeoJSON
### Any valid GeoJSON object

```json
{
  "type": "Point",
  "coordinates": [125.6, 10.1]
}
```

```json
{
  "type": "Polygon",
  "coordinates": [
    [ [100.0, 0.0], [101.0, 0.0], [101.0, 1.0], [100.0, 1.0], [100.0, 0.0] ],
    [ [100.2, 0.2], [100.8, 0.2], [100.8, 0.8], [100.2, 0.8], [100.2, 0.2] ]
  ]
}
```

---

# Arbitrary JSON
### Look for an object with geo information in it

```javascript
{
  "foo": "bar",
  "x": -122.6366, // 'long', 'lng', 'longitude'
  "y": 45.5264,   // 'lat', 'latitude'
  "radius": 100   // 'accuracy', 'acc', 'distance', 'dist', 'rad'
}

// or...

{
  "coords": [-122.6366, 45.5264] // 'coordinates', 'geo', 'loc', 'location'
}
```

---

     XXX  XXX  XXX  XXX  XX                                              +-----------------------+
    XXXXXXXXXXXXXXXXXXXXXXXX                +------------+               |                       |
    XXX                  XXX                |            |     YES       |  Add to foundGeo set  |
     X   HTTP POST JSON   X ---------+----> |  GeoJSON?  +-------------> |           &           |
    XXX                  XXX         |      |            |               |  Save path to object  |
    XXXXXXXXXXXXXXXXXXXXXXXX         |      +--------+---+               |                       |
     XXX  XXX  XXX  XXX  XX          |               |                   +-----------------------+
                                     |               | NO                            ^             
                                     |               |                               |            
                                     |               v                               |            
                                     |    +----------------------------------+       |            
                                     |    |                                  |       |            
                                     |    |  Does this object contain the    |  YES  |            
                                     |    |  information required to create  +-------+            
                                     |    |  a GeoJSON object?               |                    
                                     |    |                                  |                    
                                     |    +-------------------------+--------+                    
                                     |                              |                             
                                     |                              | NO                          
                                     |                              |                             
                                     +------------------------------+                             
                                       Iterate over keys sending                                  
                                       each value through the                                     
                                       process                                                    
![original](gophercloud.png)                                                                                                 

---

# [fit] TODO:

Describe how we started with channels and ended up with a standard mutex lock.

---

# Websockets

---

# Redis mocking

---

# Rate limiting middleware

---

# Build/deployment process

---

# Questions?

![](http://img.thesun.co.uk/multimedia/archive/01690/download__7__1690117a.gif)

---

# Thanks!

- Ryan Arana
_@aranasaurus_
github.com/aranasaurus

- Josh Yaganeh
_@hsoj_
github.com/jyaganeh

- Courtland Fowler
_@FowlerCourt_
github.com/courtf

__http://geobin.io/__

