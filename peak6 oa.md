# peak6 oa

1. airport

   - Description

     > <img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200909213832237.png" alt="image-20200909213832237" style="zoom:50%;" />
     >
     > <img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200909213859492.png" alt="image-20200909213859492" style="zoom:50%;" />
     >
     > <img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200909213915921.png" alt="image-20200909213915921" style="zoom:50%;" />

     

   - Solution

     > ```python
     > from collections import deque
     > def find(land_time, take_off_time, initial_planes, max_wait_time):
     >     size_1, size_2 = len(land_time), len(take_off_time)
     >     processed_land_time, processed_take_off_time = [], []
     >     for l_t in land_time:
     >         for t_t in take_off_time:
     >             if t_t > l_t:
     >                 processed_land_time.append(l_t)
     >                 processed_take_off_time.append(t_t)
     >                 break
     >     left_land_length = size_1 - len(processed_land_time)
     >     left_take_length = size_2 - len(processed_take_off_time)
     >     initial_planes += (left_land_length - left_take_length)
     >     land_time, take_time = deque(processed_land_time), deque(processed_take_off_time)
     >     take_off_time_on_gate = deque()
     >     take_off_time_on_gate.append(take_time.popleft())
     >     land_time.popleft()
     >     max_len = 0
     >     while land_time and take_time:
     >         max_len = max(max_len, take_off_time_on_gate)
     >         time = land_time[0] + max_wait_time
     >         while take_off_time_on_gate and time > take_off_time_on_gate[0]:
     >             take_off_time_on_gate.popleft()
     >         take_off_time_on_gate.append(take_time.popleft())
     >         land_time.popleft()
     >     return max_len + initial_planes
     > ```

2. kangroo

   - Description

     > <img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200909214526780.png" alt="image-20200909214526780" style="zoom:50%;" />
     >
     > <img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200909214543921.png" alt="image-20200909214543921" style="zoom:50%;" />
     >
     > <img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200909214601107.png" alt="image-20200909214601107" style="zoom:50%;" />
     >
     > <img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200909214621626.png" alt="image-20200909214621626" style="zoom:50%;" />
     >
     > <img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200909214637371.png" alt="image-20200909214637371" style="zoom:50%;" />
     >
     > <img src="C:\Users\gcy\AppData\Roaming\Typora\typora-user-images\image-20200909214651969.png" alt="image-20200909214651969" style="zoom:50%;" />

   - Solution

     > ```python
     > def find(s, t):
     >     size_s, size_t = len(s), len(t)
     >     i, j = 0, 0
     >     find = False
     >     while j < size_s:
     >         if t[i] == s[j]:
     >             i += 1
     >             if i == size_t:
     >                 find = True
     >         j += 1
     >     find_not_consecutive = False
     >     if find:
     >         for k in range(size_s):
     >             if s[k] == t[0]:
     >                 if s[k : k + len(t)] != t:
     >                     find_not_consecutive = True
     >                     break
     >     return find_not_consecutive
     > ```

     