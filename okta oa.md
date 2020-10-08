okta oa

- Description: https://www.1point3acres.com/bbs/thread-552371-1-1.html

- Solution:

  ```python
  import heapq
  def dvm(customers, numWindows, queueSize):
      size = len(customers)
      queue = customers[:queueSize]
      windows = [(0, i, 0) for i in range(numWindows)]
      windows = heapq.heapify(windows)
      indexOutOfQueue = queueSize
      while queue:
          firstPersonArriveTime, firstPersonServiceTime, firstPersonMaxWaitTime = queue[0].splist(',')
          firstPersonArriveTime, firstPersonServiceTime, firstPersonMaxWaitTime = int(firstPersonArriveTime), int(firstPersonServiceTime), int(firstPersonMaxWaitTime)
          mostRecentServiceTime = windows[0][0]
          # the person can not wait for the windows
          firstPersonQuitTime = firstPersonArriveTime + firstPersonMaxWaitTime
          timeLeaveQueue = min(mostRecentServiceTime, firstPersonQuitTime)
          while indexOutOfQueue < size:
              nextInQueuePersonArriveTime, nextInQueuePersonServiceTime, nextInQueuePersonMaxWaitTime = customers[indexOutOfQueue].split(',')
              nextInQueuePersonArriveTime, nextInQueuePersonServiceTime, nextInQueuePersonMaxWaitTime = int(nextInQueuePersonArriveTime), int(nextInQueuePersonServiceTime), int(nextInQueuePersonMaxWaitTime)
              if nextInQueuePersonArriveTime < timeLeaveQueue:
                  indexOutOfQueue += 1
          poppedPersonArriveTime, poppedPersonServiceTime, poppedPersonMaxWaitTime = queue.pop(0).split(',')
          poppedPersonArriveTime, poppedPersonServiceTime, poppedPersonMaxWaitTime = int(poppedPersonArriveTime), int(poppedPersonServiceTime), int(poppedPersonMaxWaitTime)
          if indexOutOfQueue < size:
              queue.append(customers[indexOutOfQueue])
          if mostRecentServiceTime <= firstPersonQuitTime:
              a, b, c = heapq.heappop(windows)
              heqpq.heappush(windows, (a + poppedPersonServiceTime, b, c + 1))
      res = [0] * (numWindows + 1)
      total = 0
      while windows:
          a, b, c = heapq.heappop()
          total += c
          res[b] = c
      res[0] = total
      return res
  
  ```

  