# 468. Validate IP Address

# Solution

这道题目判断条件比较繁琐。

```java
class Solution {
    public String validIPAddress(String IP) {
        if(isValidIPv4(IP))
            return "IPv4";
        else if(isValidIPv6(IP))
            return "IPv6";
        else
            return "Neither";
    }
    
    private boolean isValidIPv4(String IP){
        if(IP.length() < 7) return false;
        if(IP.charAt(0) == '.') return false;
        if(IP.charAt(IP.length() - 1) == '.') return false;
        String[] tokens = IP.split("\\.");
        if(tokens.length != 4) return false;
        for(String token : tokens){
            if(!isValidIPv4Token(token)) return false;
        }
        return true;
    }
    
    private boolean isValidIPv4Token(String token){
        if(token.startsWith("0") && token.length() > 1) return false;
        try{
            int parseInt = Integer.parseInt(token);
            if(parseInt < 0 || parseInt > 255) return false;
            if(parseInt == 0 && token.charAt(0) != '0') return false;
        }catch(NumberFormatException nfe){
            return false;
        }
        return true;
    }
    
    private boolean isValidIPv6(String IP){
        if(IP.length() < 7) return false;
        if(IP.charAt(0) == ':') return false;
        if(IP.charAt(IP.length() - 1) == ':') return false;
        String[] tokens = IP.split(":");
        if(tokens.length != 8) return false;
        for(String token : tokens){
            if(!isValidIPv6Token(token)) return false;
        }
        return true;
    }
    
    private boolean isValidIPv6Token(String token){
        if(token.length()==0||token.length()>4) return false;
        char[] charArray = token.toCharArray();
        for(char c : charArray){
            boolean isDigit = c>=48 && c<=57;
		    boolean isUppercaseAF = c>=65 && c<=70;
		    boolean isLowerCaseAF = c>=97 && c<=102;
            if(!(isDigit || isUppercaseAF || isLowerCaseAF)) 
                return false;
        }
        return true;
    }
}
```

