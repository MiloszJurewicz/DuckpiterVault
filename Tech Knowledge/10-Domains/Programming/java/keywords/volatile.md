#javaKeyword 
#java
value of volatile becomes visible to all readers (other threads) after write operations completes on it. Without volatile, readers could see non updated value. This ensures [[Visibility (multithreading)]]