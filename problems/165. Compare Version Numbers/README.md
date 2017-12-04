# 165. Compare Version Numbers

```java
class Solution {
    public int compareVersion(String version1, String version2) {
        String[] list1 = version1.split("\\.");
        String[] list2 = version2.split("\\.");
        if(list1.length == 0){
            list1 = new String[1];
            list1[0] = version1;
        }
        if(list2.length == 0){
            list2 = new String[1];
            list2[0] = version2;
        }
        int maxLen = Math.max(list1.length, list2.length);
        for(int i=0; i<maxLen; i++){
            int v1 = i < list1.length ? Integer.valueOf(list1[i]) : 0;
            int v2 = i < list2.length ? Integer.valueOf(list2[i]) : 0;
            if(v1 < v2)
                return -1;
            else if(v1 > v2)
                return 1;
        }
        return 0;
    }
}
```

