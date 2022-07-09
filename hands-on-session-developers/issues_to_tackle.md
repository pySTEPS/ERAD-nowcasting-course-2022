# PySteps minor issues/improvements for the hands-on activities

This section lists small issues or improvements to tackle during the hands-on activities. 

## Issues

1. [Add tests](#add-tests)
   - [Issue 1: Test that a ValueError exception is raised when the input array contains NaNs](#issue-2-test-that-input-arrays-with-more-than-2-dimensions-raise-a-valueerror-exception)
   - [Issue 2: Test that input arrays with more than 2 dimensions raise a ValueError exception](#issue-2-test-that-input-arrays-with-more-than-2-dimensions-raise-a-valueerror-exception)
   - [Issue 3: Test that a 1D-array with the coordinates' scale is accepted](#issue-3-test-that-a-1d-array-with-the-coordinates-scale-is-accepted)
   - [Issue 4: Test that a ValueError exception is raised when the input array contains NaNs](#issue-4-test-that-a-valueerror-exception-is-raised-when-the-input-array-contains-nans)
   - [Issue 5: Test that input arrays with more than 2 dimensions raise a ValueError exception](#issue-5-test-that-input-arrays-with-more-than-2-dimensions-raise-a-valueerror-exception)
   - [Issue 6: Test that input arrays with incorrect dimensions raise a ValueError exception](#issue-6-test-that-input-arrays-with-incorrect-dimensions-raise-a-valueerror-exception)
   - [Issue 7: Test that passing the timesteps raises a ValueError exception if they are not sorted in ascending order](#issue-7-test-that-passing-the-timesteps-raises-a-valueerror-exception-if-they-are-not-sorted-in-ascending-order)

3. [Code improvements](#code-improvements)

   - [Issue 8: Improve the get_method interface from the pysteps.verification.interface.py module](#issue-8-improve-the-get_method-interface-from-the-pystepsverificationinterfacepy-module)


## Add tests

Testing is a crucial part of software development. 
PySteps contains a large number of tests to make sure that the software runs as expected. Although most of the functionality is tested directly (unit-test) or indirectly (through examples), some parts of the code base are not being tested yet. Will you give us a hand? 

We have prepared the code snippets to test this functionality. Still, unfortunately, they need to be placed in the correct place (inside the corresponding test scripts) by adding a new test function containing the code snippet. Also, they may need a few adjustments since they do not entirely follow the [PySteps coding guidelines](https://pysteps.readthedocs.io/en/latest/developer_guide/contributors_guidelines.html#code-style). 

**Important**: The names of the test functions should always start with `test_`.

**Suggestion**: Use self-explanatory names for the test functions. E.g.: `test_my_function_raises_exeption_with_nans`


Here is a list of tests (and the corresponding testing snippet) that needs to be added: 

### 1. `pysteps.utils.cleansing.decluster` function

[The test coverage for this function](https://app.codecov.io/gh/pySTEPS/pysteps/compare/283/tree/pysteps/utils/cleansing.py#D1L20) indicates that some parts are not being tested. Here is a list of test that could be added (pick one!):

The following test snippets should be added to the `pysteps/tests/test_utils_cleansing.py` file:

#### [Issue 1: Test that a ValueError exception is raised when the input array contains NaNs.](https://app.codecov.io/gh/pySTEPS/pysteps/compare/283/tree/pysteps/utils/cleansing.py#D1L58)

```python
cor = np.ones((3, 1))
iarr = np.ones((3, 1))
scale = 20

iarr[1,0] = np.nan
with pytest.raises(ValueError):
    cleansing.decluster(cor, iarr, scale)
```

#### [Issue 2: Test that input arrays with more than 2 dimensions raise a ValueError exception](https://app.codecov.io/gh/pySTEPS/pysteps/compare/283/tree/pysteps/utils/cleansing.py#D1L66)


```python
c_2D = np.ones((3, 1))
c_3D = c_2D[:,None]
iarr_2D = np.ones((3, 1))
iarr_3D = iarr_2D[:, None]
scale = 20

combinations_to_test = [
    (c_3D, iarr_2D),
    (c_3D, iarr_3D),
    (c_2D, iarr_3D)
]
for coord, input_arr in combinations_to_test:
    with pytest.raises(ValueError):
        cleansing.decluster(coord, input_arr, scale)
```


#### [Issue 3: Test that a 1D-array with the coordinates' scale is accepted](https://app.codecov.io/gh/pySTEPS/pysteps/compare/283/tree/pysteps/utils/cleansing.py#D1L84)
    
```python
X = np.tile(np.random.randint(100, size=(10,2)), (3,1))
V = np.tile(np.random.randint(100, size=(10,2)), (3,1))
scale = [20,20]

X_dec, V_dec = cleansing.decluster(X, V, scale)
X_dec_ref, V_dec_ref = cleansing.decluster(X, V, scale[0])

assert X_dec.ndim == 2
assert V_dec.ndim == 2
np.testing.assert_almost_equal(X_dec, X_dec_ref)
np.testing.assert_almost_equal(V_dec, V_dec_ref)
```



### 2. `pysteps.utils.cleansing.detect_outliers` function

[The test coverage for this function](https://app.codecov.io/gh/pySTEPS/pysteps/compare/283/tree/pysteps/utils/cleansing.py#D1L123) indicates that some parts are not being tested. Here is a list of test that could be added (pick one!):

The following test snippets should be added to the `pysteps/tests/test_utils_cleansing.py` file:

#### [Issue 4: Test that a ValueError exception is raised when the input array contains NaNs.](https://app.codecov.io/gh/pySTEPS/pysteps/compare/283/tree/pysteps/utils/cleansing.py#D1L164)

```python
V = np.zeros((20, 3))
V[3, :] = np.nan
thr_std_devs = 1
with pytest.raises(ValueError):
    cleansing.detect_outliers(V, thr_std_devs, k=10)
```

#### [Issue 5: Test that input arrays with more than 2 dimensions raise a ValueError exception](https://app.codecov.io/gh/pySTEPS/pysteps/compare/283/tree/pysteps/utils/cleansing.py#D1L173)

```python
V = np.zeros((20, 3, 2))
thr_std_devs = 1
with pytest.raises(ValueError):
    cleansing.detect_outliers(V, thr_std_devs, k=10)
```

This test will raise an error! It seems that we caught a bug in the code. 

Do you want to fix it? The problem is in line #175 in the `pysteps/utils/cleansing.py` file. The wrong variable is being used in the f-string. 


### 3. `pysteps.extrapolation.semilagrangian.extrapolate` function

[The test coverage for this function](https://app.codecov.io/gh/pySTEPS/pysteps/compare/283/tree/pysteps/extrapolation/semilagrangian.py#D1L22) indicates that some parts are not being tested. Here is a list of test that could be added (pick one!):

The following test snippets should be added to the `pysteps/tests/test_extrapolation_semilagrangian.py` file:

#### [Issue 6: Test that input arrays with incorrect dimensions raise a ValueError exception](https://app.codecov.io/gh/pySTEPS/pysteps/compare/283/tree/pysteps/extrapolation/semilagrangian.py#D1L108)

For this issue, we need to corroborate that the `extrapolate` function raises a ValueError exception when the precipitation or the velocity input fields have a dimension different from 2 and 3, respectively.


```python
p_1d = np.ones(8)
p_2d = np.ones((8, 8))
p_3d = np.ones((8, 8, 2))
v_2d = np.ones((8, 8))
v_3d = np.stack([v_2d, v_2d])

num_timesteps = 1

invalid_inputs = [
    (p_1d, v_3d),
    (p_2d, v_2d),
    (p_3d, v_2d),
    (p_3d, v_3d),
]
for precip, velocity in invalid_inputs:
    with pytest.raises(ValueError):
        extrapolate(precip, velocity, num_timesteps)
```

#### [Issue 7: Test that passing the timesteps raises a ValueError exception if they are not sorted in ascending order](https://app.codecov.io/gh/pySTEPS/pysteps/compare/283/tree/pysteps/extrapolation/semilagrangian.py#D1L108)

```python
precip = np.ones((8, 8))
v = np.ones((8, 8))
velocity = np.stack([v, v])

not_ascending_timesteps = [1,2,3,5,4,6,7]
with pytest.raises(ValueError):
    extrapolate(precip, velocity, not_ascending_timesteps)
````

# Code improvements 

## Issue 8: Improve the get_method interface from the pysteps.verification.interface.py module

The `get_method` interface has a large number of nested if conditions. Some of these conditions are evaluated using the following syntax (starting from line 217): `if name in ["score_name"]:`

These can be rewritten them using a straightforward comparison: `if name == "score_name":` (without using the "in" operation).

