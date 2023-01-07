
#include <cstdlib>
#include <iostream>
#include <winsock.h>
#include <windows.h>
#include <string>
using namespace std;

void rc4(unsigned char * input, unsigned char * key,unsigned char * &output){                    
	
    unsigned char * doc;	
    int i,j=0,t,n,s[256], s2[256],temp,K;	
    
    for (i=0;i<256;i++){
	    s[i]=i;//mengisi indek
	    s2[i]= key[(i % strlen((char *)key))]; //mengisi index s2 dengan key sampai penuh
    }
    //KSA	
    for (i=0;i<256;i++){
	    j = (j + s[i] + s2[i]) % 256;
	    temp=s[i];
	    s[i]=s[j];
	    s[j]=temp;
    }
	
    doc = new unsigned char [ (int)strlen((char *)input)] ;
	//PGRA
    for (i=j=n=0;n<(int)strlen((char *)input);n++){
        i = (i + 1) % 256;
        j = (j + s[i]) % 256;
        
        temp=s[i];
        s[i]=s[j];
        s[j]=temp;//swap

        t = (s[i] + s[j]) % 256;
        K = s[t];//keyStream        
        doc[n]=input[n]^K;//XOR //ENCRIPT   //DECRIPT 
	}	
    doc[n]='\0';
    output=doc;
}


int main(int argc, char *argv[])
{
    unsigned char * plaintext;
    unsigned char * key;
    unsigned char * encrypted;
    unsigned char * decrypted;

    cout <<" PROGRAM ENKRIPSI DAN DESKRIPSI MENGGUNAKAN METODA XOR "<<endl;
	cout <<"Nama   : Dheny Ramadhana Setyarso  " <<endl;
	cout <<"NIM    : 312010396 " <<endl;
	cout <<"Kelasi : TI.20.D3 " <<endl;
	cout <<"============================================================================================" <<endl<<endl;
	
	plaintext=(unsigned char *)"Saya harus lulus tepat waktu dan menjadi sarjana"; 
    key=(unsigned char *)"kijang 90 2022";//key harus sama

    rc4(plaintext,key,encrypted);
   
    cout << "Plaintext  = " << plaintext << endl<< endl;
    cout << "Enkirpsinya =  " << encrypted << endl<< endl;
    rc4(encrypted,key,decrypted); //encrypted sbg input
    cout << "Dekripsinya =  " << decrypted << endl<< endl;
    
    return 0 ;
                 
}
