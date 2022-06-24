# Time Based Key-Value Store
---
- ## Question:
>Design a time-based key-value data structure that can store multiple values for the same key at different time stamps and retrieve the key's value at a certain timestamp.
>
>Implement the TimeMap class:
>
>- TimeMap() Initializes the object of the data structure.
>
>- void set(String key, String value, int timestamp) Stores the key key with the value value at the given time timestamp.
>
>- String get(String key, int timestamp) Returns a value such that set was called previously, with timestamp_prev <= timestamp. If there are multiple such values, it returns the value associated with the largest timestamp_prev. If there are no values, it returns ""
---
- ## Example:
>Input
>["TimeMap", "set", "get", "get", "set", "get", "get"]
>[[], ["foo", "bar", 1], ["foo", 1], ["foo", 3], ["foo", "bar2", 4], ["foo", 4], ["foo", 5]]
>
>Output
>[null, null, "bar", "bar", null, "bar2", "bar2"]
---
- ## Solution:
**Code :**
```java
class TimeValue {
    String val;
    int timestamp;
    
    public TimeValue(String val, int time){
        this.val = val;
        timestamp = time;
    }
}
class TimeMap {
    Map<String, List<TimeValue>> map;
    public TimeMap() {
        map = new HashMap<>();
    }
    
    public void set(String key, String value, int timestamp) {
        map.computeIfAbsent(key, k -> new ArrayList<>()).add(new TimeValue(value, timestamp));
    }
    
    public String get(String key, int timestamp) {
        List<TimeValue> list = map.getOrDefault(key, null);
        if(list == null) return "";
        int low = 0, high = list.size()-1;
        if(list.get(low).timestamp > timestamp) return "";
        if(list.get(high).timestamp <= timestamp) return list.get(high).val;
        while(low < high){
           int mid = (low + high) / 2;
           if(list.get(mid).timestamp == timestamp) return list.get(mid).val;
           if(list.get(mid).timestamp < timestamp) low = mid + 1;
           else high = mid - 1;
            
        }
        return list.get(low - 1).val;
        
    }
}
/**
 * Your TimeMap object will be instantiated and called as such:
 * TimeMap obj = new TimeMap();
 * obj.set(key,value,timestamp);
 * String param_2 = obj.get(key,timestamp);
 */
