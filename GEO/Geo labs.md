
## Speed filter

1. get a trajectory of the city of pisa

```
let first valid point p_valid = (lat, lng, time)
let trajectory T=(p_0, ..., p_{n-1})
let T'=[T[0]]
let speed threshold st = 0
let invalid_points = []

def speed

	for p in range(points ordered):
		d=dist(p_valid, p)
		t=time(p_valid, p)
		s=speed(d,t)
		if s < st:
			newT.append(p)
			p_valid = p
		else:
			invalid_points.add(p)
			
```


To visualize a trajectory, use scikit-mobility using a trajectory dataframe.











