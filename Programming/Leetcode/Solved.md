### Binary search
#### 153. Find Minimum in Rotated Sorted Array 
This one needed a careful pick of condition (as we not searching for target but for min). Key idea, go where min is, but keep one of the bounds = to middle (in case it is min). #solved-with-iteration
#### 33. Search in sorted rotated array
Similar to top, there are two ways - use top to find rotation and then solve using mods OR find condition based on pivot and solve like that.
Be very careful picking condition #solved-with-iteration

#### 981. Time Based Key-Value Store
Need to find closest smallest index if exists. Key was again being very careful about the bounds. #failed