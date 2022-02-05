
#  Chiffre de Vigenère
##  Introduction




Le chiffre de Vigenère est un système de chiffrement par substitution polyalphabétique dans lequel une même lettre du message clair peut, suivant sa position dans celui-ci, être remplacée par des lettres différentes, contrairement à un système de chiffrement mono alphabétique comme le chiffre de César.

![enter image description here](https://cdn.discordapp.com/attachments/403688901111447552/939329373604053002/vigenere.png)  


  

 
  # Application
  ## Chiffrement
  
Pour chaque lettre en clair, on sélectionne la colonne correspondante et pour une lettre de la clé on sélectionne la ligne adéquate, puis au croisement de la ligne et de la colonne on trouve la lettre chiffrée. La lettre de la clé est à prendre dans l'ordre dans laquelle elle se présente et on répète la clé en boucle autant que nécessaire.
 
 

- Implementation du code :
 ```c
 #include<iostream>
#include<string>
#include<cstring>
#include<algorithm>
#include<bits/stdc++.h>
using namespace std;

int getposition(const char *array, int size, char c)
{
    for (size_t i = 0; i < size; i++)
    {
        if (array[i] == c)
            return (int)i;
    }
    
}
int main() {
   string msg ;
   string key;
   cout << "msg :" << endl;
   getline(cin,msg);
   cout << "key :" << endl;
   getline(cin,key);
   msg.erase(std::remove (msg.begin(), msg.end(), ' '), msg.end());
   transform(msg.begin(), msg.end(), msg.begin(), ::toupper);
   transform(key.begin(), key.end(), key.begin(), ::toupper);

    char alphabet[26]={'A','B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R','S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'};
    char msg_array[msg.length()];
    char key_array[key.length()];
    strcpy(msg_array, msg.c_str());
    strcpy(key_array, key.c_str());
    int outm_array[msg.length()];
    int outk_array[key.length()];
    for(int i=0;i<msg.length();i++)
        outm_array[i]=getposition(alphabet,26,msg_array[i]);
    for(int i=0;i<key.length();i++)
        outk_array[i]=getposition(alphabet,26,key_array[i]);
    int out_array[msg.length()];
    for(int i=0;i<msg.length();i++)
    	out_array[i]=((outm_array[i]+outk_array[(i+1)%key.length()])+26)%26;
	
        
   
	string o_array;
    for(int i=0;i<msg.length();i++)
        o_array+=alphabet[out_array[i]];
    
   cout << msg<<endl;
   cout << o_array;
  return 0;
}
 ```
 ## Dechiffrement
 Si on veut déchiffrer ce texte, on regarde pour chaque lettre de la clé répétée la ligne correspondante et on y cherche la lettre chiffrée. La première lettre de la colonne que l'on trouve ainsi est la lettre déchiffrée.
- Implementation du code :
```c
#include<iostream>
#include<string>
#include<cstring>
#include<algorithm>
#include<bits/stdc++.h>
using namespace std;

int getposition(const char *array, int size, char c)
{
    for (size_t i = 0; i < size; i++)
    {
        if (array[i] == c)
            return (int)i;
    }
    
}
int main() {
   string msg ;
   string key;
   cout << "msg a dechiffrer :" << endl;
   getline(cin,msg);
   cout << "key :" << endl;
   getline(cin,key);
   msg.erase(std::remove (msg.begin(), msg.end(), ' '), msg.end());
   transform(msg.begin(), msg.end(), msg.begin(), ::toupper);
   transform(key.begin(), key.end(), key.begin(), ::toupper);

    char alphabet[26]={'A','B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R','S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'};
    char msg_array[msg.length()];
    char key_array[key.length()];
    strcpy(msg_array, msg.c_str());
    strcpy(key_array, key.c_str());
    int outm_array[msg.length()];
    int outk_array[key.length()];
    for(int i=0;i<msg.length();i++)
        outm_array[i]=getposition(alphabet,26,msg_array[i]);
    for(int i=0;i<key.length();i++)
        outk_array[i]=getposition(alphabet,26,key_array[i]);
    int out_array[msg.length()];
    for(int i=0;i<msg.length();i++)
    	out_array[i]=((outm_array[i]-outk_array[(i+1)%key.length()])+26)%26;
	
        
   
	string o_array;
    for(int i=0;i<msg.length();i++)
        o_array+=alphabet[out_array[i]];
    
   cout << msg<<endl;
   cout << o_array;
  return 0;
}
 ```
# ***FIN***
