# broadcast-numpy

## Compare execution time
* Without broadcasting
```python
xr_matrix = []

for i in range(num_x_vals):
    x_final_vs_r = []
    for r in r_vals:
        x = x_initial_values[i]
        for _ in range(num_timesteps):
            x = x * (1-x) * r
        x_final_vs_r.append(x)
    xr_matrix.append(x_final_vs_r)
```
Execution time: 8.315 (s)

* With broadcasting

```python
x_initial_values = np.array(x_initial_values)
r_vals = np.array(r_vals)

# x_final_vs_r = x_initial_values[:, np.newaxis]*(1-x_initial_values[:, np.newaxis])*r_vals
x_final_vs_r = (x_initial_values*(1-x_initial_values))[:, np.newaxis]*r_vals
for _ in range(num_timesteps-1):
    x_final_vs_r = x_final_vs_r*(1-x_final_vs_r)*r_vals
```
Execution time: 0.098 (s)
