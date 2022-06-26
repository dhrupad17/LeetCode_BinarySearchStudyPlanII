# Snapshot Array
---
- ## Question:
> Implement a SnapshotArray that supports the following interface:

>- SnapshotArray(int length) initializes an array-like data structure with the given length.  Initially, each element equals 0.
>- void set(index, val) sets the element at the given index to be equal to val.
>- int snap() takes a snapshot of the array and returns the snap_id: the total number of times we called snap() minus 1.
>- int get(index, snap_id) returns the value at the given index, at the time we took the snapshot with the given snap_id
---
- ## Example:
>Input: ["SnapshotArray","set","snap","set","get"]
[[3],[0,5],[],[0,6],[0,0]]

>Output: [null,null,0,null,5]
>
>Explanation: 
SnapshotArray snapshotArr = new SnapshotArray(3); // set the length to be 3
snapshotArr.set(0,5);  // Set array[0] = 5
snapshotArr.snap();  // Take a snapshot, return snap_id = 0
snapshotArr.set(0,6);
snapshotArr.get(0,0);  // Get the value of array[0] with snap_id = 0, return 5
---
- ## Solution:
**Code :**
```java
class SnapshotArray {
    public List<int[]>[] h;
    public int snap = 0;
    public SnapshotArray(int length) {
        h = new List[length];
        for (int i = 0; i < length; i++) {
            h[i] = new ArrayList<>();
            // add an initial [snap_id, val] pair, very important
            h[i].add(new int[]{-1, 0});
        }
    }
    
    public void set(int index, int val) {
        h[index].add(new int[]{snap, val});
    }
    
    public int snap() {
        return snap++;
    }
    
    public int get(int index, int snap_id) {
        List<int[]> temp = h[index];
        int l = 0, r = temp.size() - 1;
        // binary search rightmost
        while (l < r) {
            int m = r - (r - l) / 2;
            if (temp.get(m)[0] <= snap_id) l = m;
            else r = m - 1;
        }
        return temp.get(l)[1];
    }
}
