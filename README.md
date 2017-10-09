#include<iostream>
#include<queue>
#include<algorithm>
using namespace std;
int tree[1000001];
// a,b -> actual range
void build_tree(vector<int> A, int node, int a, int b) {
    if (a == b) { 
        tree[node] = A[a]; 
    }
    else {
        int leftChild, rightChild, middle;
        leftChild=2*node;
        rightChild=2*node+1;
        middle=(a+b)/2;
        build_tree(A,leftChild,a,middle); 
        build_tree(A,rightChild,middle+1,b); 
        tree[node]=max(tree[leftChild], tree[rightChild]); 
    }
}
int query(int node, int a, int b, int p, int q) {
    if (p >= a && b >= q) 
        return tree[node];
    int l, r, m;
    l=2*node;
    r=l+1;
    m=(a+b)/2;
    return max(query(l,a,m,p,q),query(r,m+1,b,p,q)); 
}
int main(){
    int n,m;
    cin >> n >> m;
    vector<int> a;
    int input;
    int left=0,right=0;
    for(int i=1;i<=n;i++){
        cin >> input;
        a.push_back(input);
    }
    build_tree(a,1,1,n);
    for(int i=1;i<=m;i++){
        cin >> left >> right;
        query(1,left,right,1,n);
    }
}
