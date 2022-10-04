# Tournament-Organizer
/*

date: MAR 24, 2021
author: Asumi
purpose: This program is to organize a tournament involving n competitors.
*/

import java.util.Scanner;
class Recursion {
    final int MAXR = 32; 
    final int MAXC = 32;
    int a [][]; 
    int nR, nC;

    //constructor
    Recursion() {
        a = new int[MAXR][MAXC];
        nR = 1;
        nC = 0;
    }

    public void setA(int[][] array){
	a = array;
    }

    public int[][] getA(){
	return a;
    }

    public void setNR(int r){
	nR = r;
    }
   
    public int getNR(){
	return nR;
    }

    public void setNC(int c){
	nC = c;
    }
   
    public int getNC(){
	return nC;
    }

    //get methods only for our constants MAXR and MAXC
    public int getMAXR(){
	return MAXR;
    }
    
    public int getMAXC(){
	return MAXC;
    }

    void printA() {
        System.out.printf("%18s", "Player");
        System.out.println();
        System.out.printf("%4s", "Day");
        printA(nC-1);
    }

    void printA(int n) {
        if (n >= 0) {
            printA(n-1);
            if (n == 0)
                System.out.printf("%6s", "");
            if (n >= 1)
                System.out.printf("%10s", "d"+n);
            for (int c = 0; c < nC; c++)
                System.out.printf("%3d", (a[n][c]));
            System.out.println();
        }
    }
    
    void buildSchedule(int n) {
        if (n >= 1) {
            buildSchedule(n/2);
            int c = 0;
            for (int i = 0; i< nC; i+= (2*n)) {
                for (int j = 0; j< n; j++)
                    a[nR][c+j] = a[nR-n][c+j+n];
                for (int j = n; j < n*2; j++)
                    a[nR][c+j] = a[nR-n][c+j-n];
                c+=2*n;
            }
            nR++;
            if (n > 1)
                buildSchedule(n/2);
        }
    }
}

public class Tournament-Organizer {
    static boolean isPow(int n) {
        while (n>1) {
            if(n%2!=0)
                return false;
            n/=2;
        }
        return true;
    }

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int p;
        
        do {
            System.out.print("How many player you want to set? (0 to exit): ");
            p = in.nextInt();

            do {
                if (isPow(p) == false) {
                    System.out.println("You must put a power of 2 number.");
                    System.out.print("How many player you want to set? (0 to exit): ");
                    p = in.nextInt();
                }
            } while(isPow(p) == false);

            Recursion r = new Recursion();
            for (int i = 0; i< p; i++)
                r.a[0][i] = i+1;
                r.nC = p;

            r.buildSchedule(p/2);
            r.printA();
            System.out.println();
        } while (p > 0);
    }
}
