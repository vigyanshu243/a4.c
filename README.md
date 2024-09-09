#include <stdio.h>
#include <stdlib.h>


struct TreeNode {
    int val;
    struct TreeNode *left;
    struct TreeNode *right;
};

struct TreeNode* createNode(int value) {
    struct TreeNode* newNode = (struct TreeNode*)malloc(sizeof(struct TreeNode));
    newNode->val = value;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}
struct TreeNode* mergeTrees(struct TreeNode* t1, struct TreeNode* t2) {
   
    if (!t1) return t2;
    if (!t2) return t1;
    struct TreeNode* merged = createNode(t1->val + t2->val);
    merged->left = mergeTrees(t1->left, t2->left);
    merged->right = mergeTrees(t1->right, t2->right);

    return merged;
}


void inorderTraversal(struct TreeNode* root) {
    if (root == NULL) {
        return;
    }
    inorderTraversal(root->left);
    printf("%d ", root->val);
    inorderTraversal(root->right);
}


int main() {
    
    struct TreeNode* t1 = createNode(1);
    t1->left = createNode(3);
    t1->right = createNode(2);
    t1->left->left = createNode(5);

    struct TreeNode* t2 = createNode(2);
    t2->left = createNode(1);
    t2->right = createNode(3);
    t2->left->right = createNode(4);
    t2->right->right = createNode(7);

  
    struct TreeNode* mergedTree = mergeTrees(t1, t2);

   
    printf("Merged tree (in-order): ");
    inorderTraversal(mergedTree);
    printf("\n");

    return 0;
}
