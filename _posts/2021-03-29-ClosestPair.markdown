---
layout: single
title:  "ClosestPair"
date:   2021-03-29 03:57:49 +0900
categories: algorithm closestpair
---
ClosestPair의 가장 간단한 방법을 이용한 소스코드. 좌표를 배열을 통해 입력시키고 가장 가까운 거리와 그 때 이루는 점들의 쌍을 표현합니다.

{% highlight ruby %}
import java.util.Random;
import java.util.Scanner;

class point{
    int x;
    int y;
    public point(int x,int y){
        this.x = x;
        this.y = y;
    }
}

class Sorter{
    private void merge(point[] p, int n, int k, int m){
        point[] C = new point[m-n+1];

        int i = n, j= k+1, t=0;
        while(i<=k && j<=m) C[t++] = p[i].x < p[j].x ? p[i++] : p[j++];
        while(i<=k) C[t++] = p[i++];
        while(j<=m) C[t++] = p[j++];

        for(int a=n, b=0; a<=m; a++) p[a] = C[b++];
    }

    public void mergeSort(point p[],int n,int m){
        if(n >= m) return;
        int k = (n+m) / 2;
        mergeSort(p, n, k);
        mergeSort(p, k+1, m);
        merge(p, n, k, m);
    }
}

public class sort {

//    private void measure_distance(point[] p,int n,int m,double min){
//        for(int i = n; n<m; n++) {
//            double distance = Math.sqrt(Math.pow(p[m].x - p[n].x, 2) + Math.pow(p[m].y - p[n].y, 2));
//            if (min > distance)
//                min = distance;
//        }
//    }
//
//    private void min_distance(point[] p, int n, int k, int m,double min){
//        double x1 = p[k].x - min;
//        double x2 = p[k].x + min;
//        }
//    }
//
//    public void divide(point[] p, int n,int m,double min){
//        if(m-n <= 3){
//            measure_distance(p,n,m,min);
//            return;
//        };
//        int k = (n+m)/2;
//        divide(p,n,k,min);
//        divide(p,k+1,m,min);
//        min_distance(p,n,k,m,min);
//    }

    public static void main(String[] args) {
        Random r = new Random();
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();

        point[] p = new point[n];

        for (int i = 0; i < p.length; i++)
            p[i] = new point(sc.nextInt(), sc.nextInt());
        for (int i = 0; i < p.length; i++)
            System.out.printf("(%d,%d) ", p[i].x, p[i].y);

        Sorter sorter = new Sorter();
        sorter.mergeSort(p,0,p.length-1);

        System.out.println("");
        for (int i = 0; i < p.length; i++)
            System.out.printf("(%d,%d)", p[i].x, p[i].y);
        System.out.println("");
        double min = Math.sqrt(Math.pow(p[p.length-1].x-p[0].x,2)+Math.pow(p[p.length-1].y-p[0].y,2));
        System.out.printf("%f",min);


        double CPx1 = 0, CPx2=0, CPy1=0,CPy2=0;

        for(int i = 0; i<p.length; i++) {
            for(int j = i+1; j<p.length; j++){
                double distance = Math.sqrt(Math.pow(p[j].x - p[i].x, 2) + Math.pow(p[j].y - p[i].y, 2));
                if (min > distance) {
                    CPx1=p[i].x;
                    CPy1=p[i].y;
                    CPx2=p[j].x;
                    CPy2=p[j].y;
                    min = distance;

                }
            }
        }

        System.out.println("");
        System.out.printf("최근점의 쌍은 (%f, %f), (%f, %f)입니다. ",CPx1,CPy1,CPx2,CPy2);


        System.out.println("");
        System.out.printf("최소 거리는 %f입니다. ",min);

//        System.out.println();
//        System.out.printf("%f",min);
//
//        Closest_pair Closestpair = new Closest_pair();
//
//        Close     stpair.divide(p, 0,p.length-1, min);
//
//        System.out.println();
//        System.out.printf("%f",min);
    }
}
{% endhighlight %}

출처 : 최태성 코드