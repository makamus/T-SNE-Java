[![Build Status](https://travis-ci.org/lejon/T-SNE-Java.svg?branch=master)](https://travis-ci.org/lejon/T-SNE-Java)

T-SNE-Java
==========

NEWS 2016-11-02!
================
*T-SNE-Java now have support for __Barnes Hut__ which makes it possible to run the amazing t-SNE on much larger datasets (or much faster on small datasets:) )!*

The Barnes Hut version can also be run in parallel!

There are still many improvements possible and no optimization has been done yet. But it is already much much faster than the standard t-SNE.
Great research by Dr. Maaten!!

About
=====

Pure Java implementation of Van Der Maaten and Hinton's t-SNE clustering algorithm.

This project is divided into two separate Maven projects, one for the core t-SNE and one for the demos (stand-alone executables that can be run from command line).

With (parallel) Barnes Hut, T-SNE-Java is now in version v2.1.0, both core and demos.

Basic command line usage
------------------------

If you just want to use TSne as a command line tool, you should use BarnesHutTSneCsv for the 
Barnes Hut version or TSneCsv for the classic version. 

You must then first build and install 'tsne' and  'tsne-demos' (mvn install).
Then use the tsne-demos JAR you just build according to the examples below. 

You can also download the pre-build binary JAR from the release page.

Examples:

Run TSne on file without headers and no labels.
```shell
java -jar target/tsne-demos-2.1.0.jar -nohdr -nolbls src/main/resources/datasets/iris_X.txt 
```
Run TSne on CSV file with headers and label column nr. 5.
```shell
java -jar target/tsne-demos-2.1.0.jar --lblcolno 5 src/main/resources/datasets/iris.csv
```
Run TSne on file without headers and no labels but supply a separate label file (with the same ordering as the data file).
```shell
java -jar target/tsne-demos-2.1.0.jar --nohdr --nolbls --label_file=src/main/resources/datasets/iris_X_labels.txt src/main/resources/datasets/iris_X.txt
```

Same as above but using parallelization.
```shell
java -jar target/tsne-demos-2.1.0.jar --parallel --nohdr --nolbls --label_file=src/main/resources/datasets/iris_X_labels.txt src/main/resources/datasets/iris_X.txt
```
To see graphs generated with this implementation, [Klick here](http://lejon.github.io/TSneJava/)

For some tips working with t-sne [Klick here] (http://lejon.github.io)

Basic code usage: 
-----------------

```java
import java.io.File;

import com.jujutsu.tsne.FastTSne;
import com.jujutsu.tsne.TSne;
import com.jujutsu.utils.MatrixOps;
import com.jujutsu.utils.MatrixUtils;

public class TSneTest {
  public static void main(String [] args) {
    int initial_dims = 55;
    double perplexity = 20.0;
    double [][] X = MatrixUtils.simpleRead2DMatrix(new File("src/main/resources/datasets/mnist2500_X.txt"), "   ");
    System.out.println(MatrixOps.doubleArrayToPrintString(X, ", ", 50,10));
    TSne tsne = new FastTSne();
    double [][] Y = tsne.tsne(X, 2, initial_dims, perplexity);   

    // Plot Y or save Y to file and plot with some other tool such as for instance R

  }
}
```

To use the Barnes Hut version:

```java
import java.io.File;

import com.jujutsu.tsne.TSne;
import com.jujutsu.tsne.barneshut.BarnesHutTSne;
import com.jujutsu.utils.MatrixOps;
import com.jujutsu.utils.MatrixUtils;

public class TSneTest {
  public static void main(String [] args) {
    int initial_dims = 55;
    double perplexity = 20.0;
    double [][] X = MatrixUtils.simpleRead2DMatrix(new File("src/main/resources/datasets/mnist2500_X.txt"), "   ");
    System.out.println(MatrixOps.doubleArrayToPrintString(X, ", ", 50,10));
    TSne tsne = new BarnesHutTSne();
    double [][] Y = tsne.tsne(X, 2, initial_dims, perplexity);   
    
    // Plot Y or save Y to file and plot with some other tool such as for instance R
  }
}

```

Version
-------
Demo: 2.1.0

Core: 2.1.0

Enjoy!
-Leif
  
