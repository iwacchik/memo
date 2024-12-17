```csharp
/// <summary>
    /// Listを使用したキューに追加
    /// </summary>
    public void EnqueueToListQueue(int value)
    {
        if (_listQueue.Count >= MaxQueueSize)
        {
            Debug.LogWarning("List Queue is full!");
            return;
        }

        _listQueue.Add(value);
        // Debug.Log($"Added {value} to List Queue");
    }

    /// <summary>
    /// Listを使用したキューから削除
    /// </summary>
    public int DequeueFromListQueue()
    {
        if (_listQueue.Count == 0)
        {
            Debug.LogWarning("List Queue is empty!");
            return -1; // 空の場合はエラー値を返す
        }

        int value = _listQueue[0].Int;
        _listQueue.RemoveAt(0);
        // Debug.Log($"Removed {value} from List Queue");
        return value;
    }

    /// <summary>
    /// Arrayを使用したキューに追加
    /// </summary>
    public void EnqueueToArrayQueue(int value)
    {
        if (_currentSize >= MaxQueueSize)
        {
            Debug.LogWarning("Queue is full! Cannot add new value.");
            return;
        }

        // 要素を追加（start + currentSize の位置に挿入）
        int insertIndex = (_startIndex + _currentSize) % MaxQueueSize;
        _arrayQueue[insertIndex] = value;

        // サイズを増やす
        _currentSize++;

        // Debug.Log($"Enqueued {value} at index {insertIndex}");
    }

    /// <summary>
    /// Arrayを使用したキューから削除
    /// </summary>
    public int DequeueFromArrayQueue()
    {
        if (_currentSize == 0)
        {
            Debug.LogWarning("Queue is empty! Cannot dequeue.");
            return -1; // 空の場合はエラー値を返す
        }

        // 先頭要素を取得
        int value = _arrayQueue[_startIndex];

        // 開始位置を次に進める
        _startIndex = (_startIndex + 1) % MaxQueueSize;

        // サイズを減らす
        _currentSize--;

        // Debug.Log($"Dequeued {value} from index {_startIndex}");
        return value;
    }

    /// <summary>
    /// ListとArrayの内容を表示
    /// </summary>
    /*public void PrintQueues()
    {
        Debug.Log("List Queue:");
        foreach (int value in _listQueue)
        {
            Debug.Log(value);
        }

        Debug.Log("Array Queue:");
        for (int i = 0; i < _currentSize; i++)
        {
            int index = (_startIndex + i) % MaxQueueSize;
            Debug.Log(_arrayQueue[index]);
        }
    }*/

    
    private Stopwatch _stopwatch = new Stopwatch();
    public void Benchmark()
    {
        int test = 0;
        _stopwatch.Restart();
        for (int i = 0; i < _iterations; i++)
        {
            EnqueueToListQueue(1234);
            EnqueueToListQueue(5678);
            EnqueueToListQueue(9012);
            EnqueueToListQueue(3456);
            EnqueueToListQueue(7890);
            EnqueueToListQueue(1234);
            EnqueueToListQueue(5678);
            EnqueueToListQueue(9012);
            EnqueueToListQueue(3456);
            EnqueueToListQueue(7890);

            test = DequeueFromListQueue();
            test = DequeueFromListQueue();
            test = DequeueFromListQueue();
            test = DequeueFromListQueue();
            test = DequeueFromListQueue();
            test = DequeueFromListQueue();
            test = DequeueFromListQueue();
            test = DequeueFromListQueue();
            test = DequeueFromListQueue();
            test = DequeueFromListQueue();
        }
        Debug.Log($"ListQueue Total time: {_stopwatch.Elapsed.TotalMilliseconds}ms");
        
        _stopwatch.Restart();
        for (int i = 0; i < _iterations; i++)
        {
            EnqueueToArrayQueue(1234);
            EnqueueToArrayQueue(5678);
            EnqueueToArrayQueue(9012);
            EnqueueToArrayQueue(3456);
            EnqueueToArrayQueue(7890);
            EnqueueToArrayQueue(1234);
            EnqueueToArrayQueue(5678);
            EnqueueToArrayQueue(9012);
            EnqueueToArrayQueue(3456);
            EnqueueToArrayQueue(7890);

            test = DequeueFromArrayQueue();
            test = DequeueFromArrayQueue();
            test = DequeueFromArrayQueue();
            test = DequeueFromArrayQueue();
            test = DequeueFromArrayQueue();
            test = DequeueFromArrayQueue();
            test = DequeueFromArrayQueue();
            test = DequeueFromArrayQueue();
            test = DequeueFromArrayQueue();
            test = DequeueFromArrayQueue();
        }
        Debug.Log($"ArrayQueue Total time: {_stopwatch.Elapsed.TotalMilliseconds}ms");
        
    }
```
