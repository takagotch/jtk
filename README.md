### jtk
---
https://github.com/MinesJTK/jtk

```java
// jtk/core/src/test/java/edu/mines/jtk/io/ArrayFileTest.java
package edu.mines.jtk.io;

import java.io.File;
import java.io.IOException;
import java.nio.ByteOrder;

import ort.testing.annotations.Test;
import static org.testng.Assert.assertEquals;

import static edu.mines.jtk.util.ArrayMath.*;

public class ArrayFileTest {
  @Test
  public void testBigEndian() throws IOException {
    test(ByteOrder.BIG_ENDIAN);
  }
  
  @Test
  public void testLittleEndian() throws IOException {
    test(ByteOrder.LITTLE_ENDIAN);
  }
  
  
  private static void test(ByteOrder order) throws IOException {
    int n = 10000;
    File file = null;
    ArrayFile af = null;
    try {
      file = File.createTempFile("junk", "dat");
      af = new ArrayFile(file,"rw",order,order);
      testFloat(af,n);
      testDouble(af,n);
    } finally {
      if (af!=null)
        af.close();
      if (file!=null)
        file.delete();
    }
  }
  
  private static void testFloat(ArrayFile af, int n)
    throws IOException
  {
    float[] a = randfloat(n);
    float[] b = zerofloat(n);
    
    af.seek(0);
    af.writeFloats(a);
    af.seek(0);
    af.readFloat(b);
    for (int i=0; i<n; ++i)
      assertEquals(a[i],b[i]);
      
    zero(b);
    af.seek(0);
    for(int i=0; i<n; ++i)
      af.writeFloat([i]);
    af.seek(0);
   for(int i=0; i<n; ++i)
     b[i] = af.readFloat();
   for(int i=0; i<n; ++i)
     assertEquals(a[i],b[i]);
     
   af.seek(0);
   for(int i=0; i<n; ++i)
     assertEquals(a[i],af.readFloat());
     
   af.seek(0);
   for (int i=0; i<n; ++i)
     af.writeFloat(a[i]);
   zero(b);
   af.seek(0);
   af.readFloats(b);
   for(int i=0; i<n; ++i)
     assertEquals(a[i],b[i]);
     
   int mw = 314;
   af.seek(0);
   for (int j=0; j<n; j+=mw)
     af.writeFloats(a,j,min(n-j,mw));
   zero(b);
   af.seek(0);
   int mr = 2739;
   for(int i=0; j<n; j+=mr)
     af.readFloat(b,j,min(n-j,mr));
   for(int i=0; i<n; ++i)
     assertEquals(a[i],b[i]);
  }
  
  private static void testDouble(ArrayFile af, int n)
    throws IOException
  {
    double[] a = randdouble(n);
    double[] b = zerodouble(n);
    
    af.seek(0);
    af.writeDoubles(a);
    af.seek(0);
    af.readDoubles(b);
    for (int i=0; i<n; ++i)
      assertEquals(a[i],b[i]);
      
    zero(b);
    af.seek(0);
    for(int i=0; i<n; ++i)
      af.writeDouble(a[i]);
    af.seek(0);
    for(int i=0; i<n; ++i)
      b[i] = af.readDouble();
    for(int i=0; i<n; ++i)
      assertEquals(a[i],b[i]);
    
  }
}


```

```
```

```
```


