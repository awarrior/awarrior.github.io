---
layout: post
title: Morris Binary Tree
description: 
category: DATA STRUCTURE
---

### Describe

Besides the realization of tradictional binary tree based on recursion or stack, which needs O(n) space complexity, there also exit one structure using O(1) space complexity called Morris Binary Tree. This structure utilizes the right pointer of each leaf node to realize the searching order.

### Code

{% highlight c++ %}
// in-order
void morrisInorder() {
	node *it = &root;
	while(it) {
		if (it->left) {
			node *tend = it->left;
			while (tend->right && tend->right!=it) {
				tend = tend->right;
			}
			if (tend->right) {
				cout<<' '<<it->val;
				// tend->right = NULL;
				it = it->right;
			} else {
				tend->right = it;
				it = it->left;
			}
		} else {
			cout<<' '<<it->val;
			it = it->right;
		}
	}
	cout<<endl;
}
{% endhighlight %}

{% highlight c++ %}
// pre-order
void morrisPreorder() {
	node *it = &root;
	while(it) {
		cout<<' '<<it->val;
		if (it->left) {
			node *tend = it->left;
			while (tend->right && tend->right!=it) {
				tend = tend->right;
			}
			tend->right = it->right;
			it = it->left;
		} else {
			it = it->right;
		}
	}
	cout<<endl;
}
{% endhighlight %}

{% highlight c++ %}
// post-order
void reversePrint(node *begin, node *end) {
	node *it = begin;
	if (it == end) {
		cout<<' '<<it->val;
		return;
	}
	node *head = new node{0,NULL,NULL};
	do {
		node *nnode = new node{it->val,NULL,NULL};
		nnode->right = head->right;
		head->right = nnode;
		it = it->right;
	} while (it != end);
	cout<<' '<<it->val;
	it = head->right;
	while (it) {
		cout<<' '<<it->val;
		it = it->right;
	}
}

void morrisPostorder() {
	node *it = new node{0,&root,NULL};
	while(it) {
		if (it->left) {
			node *tend = it->left;
			while (tend->right && tend->right!=it) {
				tend = tend->right;
			}
			if (tend->right) {
				node *tmp = it->left;
				reversePrint(tmp, tend);
				it = it->right;
			} else {
				tend->right = it;
				it = it->left;
			}
		} else {
			// cout<<' '<<it->val;
			it = it->right;
		}
	}
	cout<<endl;
}
{% endhighlight %}

Example: 
{% highlight c++ %}
struct node {
	int val;
	struct node *left;
	struct node *right;
} root;

int tree[] = {0,6,2,7,1,4,0,9,0,0,3,5,0,0,8,0};
node* ptree[7];

void build() {
	root.val = tree[1];
	node *p = &root;
	ptree[1] = p;
	for (int i=1; i<=7; ++i) {
		p = ptree[i];
		if (tree[2*i] != 0) {
			p->left = new node{tree[2*i],NULL,NULL};
			ptree[2*i] = p->left;
		}
		if (tree[2*i+1] != 0) { 
			p->right = new node{tree[2*i+1],NULL,NULL};
			ptree[2*i+1] = p->right;
		}
	}
}

void print(const node* p) {
	if (!p)
		return;
	print(p->left);
	cout<<' '<<p->val;
	print(p->right);
}

int main() {
	build();
	// print(&root);
	// cout<<endl;

	morrisInorder();
	// morrisPreorder();
	// morrisPostorder();
	return 0;
}
{% endhighlight %}


