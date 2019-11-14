#include <bits/stdc++.h>
using namespace std;

struct trienode{
    bool is_word;
    trienode* child[26];
    
};

trienode* get_new_node()
{
    trienode* temp = new trienode;
    temp->is_word = false;
    
    for(int i=0;i<26;i++)    
    {
        temp->child[i] = NULL;
    }
    
    return temp;
}

void insert(trienode* root,string key)
{
    trienode* temp = root;
    
    for(int i=0;i<(int)key.length();i++)
    {
        int ind = int(key[i])-'a';
        if( temp->child[ind] == NULL )
        {
            temp->child[ind] = get_new_node();
        }
        temp = temp->child[ind];
    }
    
    temp->is_word = true;
}

bool search(trienode* root,string key)
{   
    if( root == NULL) return  false;
    trienode* temp = root;
    
    for(int i=0;i<(int)key.length();i++)
    {
        int ind = int(key[i])-'a';
        if( temp->child[ind] == NULL ) return false;
        temp = temp->child[ind];
    }
    
    return temp->is_word;
    
}

trienode* helper(trienode* root,string key,int ind)
{   // if tree is empty
    if(root==NULL) return NULL;
    
    /*
        helper function takes 3 parameters
        1) root of subtrie (or subtree)
        2) processing key (key which is going to be deleted)
        3) ind (index) -> which character is processing or how much depth
        
        it returns root of this subtrie
    */
    
    bool isempty = true;
    for(int i=0;i<26;i++)
    {
        if(root->child[i] != NULL)
        {
            isempty = false;
            break;
        }
    }
    
    if(ind == key.length())
    {
        /* hit the end of key
        
         possibilty -> 1) this key is prefix of other key, 
         int this case,set is_word of current root equals to false;
        
         possibilty ->2) this key is not prefix of any other key
         in this case delete this node;
        */
        if(isempty==false)
        {
            // case 1
            root->is_word = false;
            
        }
        else
        {
            //case 2
            delete(root);
            root = NULL;
        }
        
        return root;
        
    }
    int pos = int(key[ind])-'a';
    root->child[pos] = helper(root->child[pos],key,ind+1);
    
    isempty = true;
    for(int i=0;i<26;i++)
    {
        if(root->child[i] != NULL)
        {
            isempty = false;
            break;
        }
    }
    
    /* here we have two case
     1) if all  child nodes of root is empty and this root is not marked as 
        of word then delete this node 
    
     2) if all child nodes are not empty "OR" this root os marked as end of 
        word then do nothing
    */
    
    if( isempty && root->is_word == false )
    {
        delete(root);
        root = NULL;
    }
    
    return root;
}


trienode* delete_key(trienode* root , string key)
{   /* if trie is empty */
    if(root == NULL) return root;
    
    /* if key is empty */
    if(key == "") return root;
    
    
    /* delete_key function takes two parameters
      1) root of trie
      2) key to be deleted
      
      delete_key function returns root of modified trie 
    */
    
     root = helper( root,key,0 );
    return root;
}

void find_all_words( trienode* root,string key,vector<string>&all_words)
{
	if(root==NULL) return ;
	trienode* temp = root;
     
     for(int i=0;i<(int)key.size();i++)
     {
     	int ind = int(key[i])-'a';
     	/* if child node at ind of current root is NULL this prefix do not exist in trie  */
     	if( temp->child[ind] == NULL ) return ;
     	
     	temp = temp->child[ind];
     }
     
     /* if this prefix exist in trie then do BFS from current node to find all words  */
     queue<pair<trienode*,string> > q;
     q.push(make_pair(temp,key));
     string this_word;
     while(!q.empty())
     {
     	temp = q.front().first;
     	this_word = q.front().second;
     	/* if this is word ,then add it to the all_words(vector) */
     	if(temp->is_word) all_words.push_back( this_word );
     	q.pop();
     	for(int i=0;i<26;i++)
     	{
     		if( temp->child[i] !=NULL )
     		{
     			q.push( make_pair( temp->child[i] , this_word+char(i+int('a')) ) );
     		}
     	}
     }
	
}

void auto_complete(trienode* root, string key)
{    
	/* this function takes two parametes
	   1.) root node of trie
	   2.) key for which suggestion need to find.
	   
	   this function prints all the words for which key is prefix.
	*/
	
	/* if key is empty , no need to print */
	if(key.size() == 0) return ;
	
	/* if key is not empty , then we will print all words in trie for which key is PREFIX. */
	
	vector<string> all_words;
	
	find_all_words(root,key,all_words);
	
	/* print all words */
	
	if( all_words.size() == 0  ) 
	{
		cout<<"There are no suggestions."<<'\n';
		return ;
	}
	
	cout<<"There are "<<all_words.size()<<" suggestions for this prefix "<<key<<'\n';
	for(int i=0;i<(int)all_words.size();i++){
		cout<<all_words[i]<<' ';
	}
	
	return ;
}

int main() 
{    
	/* creating dictionary*/
	int n;
     cin>>n;
	vector<string> dict;
	string key;
	for(int i=0;i<n;i++)
	{
	    cin>>key;
	    dict.push_back(key);
	}
	/* creats root node*/
	trienode* root = get_new_node();
  
     /* inserts all words of dictionary to trie*/ 
	for(int i=0;i<dict.size();i++)
	{   
	   insert(root,dict[i]);
     }
    
    
    cout<<"Enter key to autocomplete :"<<'\n';
    cin>>key ;
    auto_complete(root,key);
	return 0;
}
