# 271. Encode and Decode Strings

```java
public class Codec {

    // Encodes a list of strings to a single string.
    public String encode(List<String> strs) {
        StringBuffer out = new StringBuffer();
        for (String s : strs)
            out.append(s.replace("#", "##")).append(" # ");
        return out.toString();
    }

    // Decodes a single string to a list of strings.
    public List<String> decode(String s) {
        List strs = new ArrayList();
        String[] array = s.split(" # ", -1);
        for (int i=0; i<array.length-1; ++i)
            strs.add(array[i].replace("##", "#"));
        return strs;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.decode(codec.encode(strs));
```

