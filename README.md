# CSC2431_Templeted_BinarySearchTree
#pragma once
#include <cassert>
#include <iostream>
#include<string>
#include <queue>
using namespace std;



namespace SPU {
	namespace CSC2431 {
		namespace Homework4 {

		template <class T>
		class BinarySearchTree
		{
		protected:
			template <class T>
			struct node
			{
				T item;
				node<T> *left;
				node<T> *right;
			};

			node<T> *root = NULL;

		public:

	
			node<T>* NewLeaf(T data)
			{
				node<T> *NewLeaf = new node<T>;
				NewLeaf->item = data;
				NewLeaf->left = NULL;
				NewLeaf->right = NULL;
				return NewLeaf;
			}

			// Adds a value to the tree
			void Add(T data) 
			{
				AddNew(data, root);
			};

			void AddNew(T data, node<T>* ptr)
			{
				if (root == NULL)
				{
					root = NewLeaf(data);
				}
				else if (data < ptr->item)
				{
					if (ptr->left != NULL)
					{
						AddNew(data, ptr->left);
					}
					else
					{
						ptr->left = NewLeaf(data);
					}
				}
				else if (data > ptr->item)
				{
					if (ptr->right != NULL)
					{
						AddNew(data, ptr->right);
					}
					else
					{
						ptr->right = NewLeaf(data);
					}
				}
			};

			// traverses the tree: preorder
			void PreorderDFS(void (*call) (T&))
			{
				PreTraverse(root, call);
			}

			// traverses the tree: postorder
			void PostorderDFS(void (*call) (T&))
			{
				PostTraverse(root, call);
			}

			// traverses the tree: inorder
			void InorderDFS(void(*call) (T&))
			{
				InTraverse(root, call);
			}
			
			// traverses the tree: breadth first
			void BFS(void(*call) (T&))
			{
				BFSTraverse(root, call);
			}



			void PreTraverse(node<T>* ptr, void(*call) (T&))
			{
				if (ptr != NULL)
				{
					call(ptr->item);
				}
				if (ptr->left != NULL)
				{
					PreTraverse(ptr->left, call);
				}
				if (ptr->right != NULL)
				{
					PreTraverse(ptr->right, call);
				}
			};

			void PostTraverse(node<T>* ptr, void(*call) (T&))
			{
				if (ptr != NULL)
				{
					if (ptr->left != NULL)
					{
						PostTraverse(ptr->left, call);
					}
					if (ptr->right != NULL)
					{
						PostTraverse(ptr->right,call);
					}
					call(ptr->item);
				}
			};

			void InTraverse(node<T>* ptr, void(*call) (T&))
			{
				if (ptr->left != NULL)
				{
					InTraverse(ptr->left, call);
				}
				if (ptr != NULL)
				{
					call(ptr->item);
				}
				if (ptr->right != NULL)
				{
					InTraverse(ptr->right, call);
				}
			};

			void BFSTraverse(node<T> *ptr, void(*call) (T&))
			{
				if (ptr == NULL) return;
				queue<node<T>*> Q;
				Q.push(ptr);
				//while there is at least one discovered node
				while (!Q.empty()) {
					node<T>* current = Q.front();
					Q.pop(); // removing the element at front
					call(current->item);
					if (current->left != NULL) Q.push(current->left);
					if (current->right != NULL) Q.push(current->right);
				}
			}


			};

		template <class T>
		void AccumulatePrint(T &data)
		{
			static T total;
			total = total + data;
			cout << total << "\t";
		}

		void Capitalize(string &data)
		{
			for (unsigned int i = 0; i < data.length(); i++)
				data.at(i) = toupper(data.at(i));
		}
		}; // Homework4
	}; // CSC2431
} // SPU
