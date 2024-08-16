  - FontMetrics   文字的 5 条 线   
      - 基准点是baseline
      - Ascent是baseline之上至字符最高处的距离
      - Descent是baseline之下至字符最低处的距离
      - Leading文档说的很含糊，其实是上一行字符的descent到下一行的ascent之间的距离
      - Top指的是指的是最高字符到baseline的值，即ascent的最大值
      - 同上，bottom指的是最下字符到baseline的值，即descent的最大值  
      - 高度
      ```Paint.FontMetricsInt fm = paint.getFontMetricsInt();  
         int top = baseLineY + fm.top;  
         int bottom = baseLineY + fm.bottom;  
         //所占高度  
         int height = bottom - top;  
      -  宽度
        ```int width = paint.measureText(String text);  
      - 最小矩形 public void getTextBounds(String text, int start, int end, Rect bounds);  
         获取指定字符串所对应的最小矩形，以（0，0）点所在位置为基线 
         - text  要测量最小矩形的字符串 
         -  start 要测量起始字符在字符串中的索引 
         - end   所要测量的字符的长度 
         - bounds 接收测量结果 