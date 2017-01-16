# Python-Study
class Node:
    """ A node in a BST. It may have left and right subtrees """
    def __init__(self, item, left = None, right = None):
        self.item = item
        self.left = left
        self.right = right

class BST:
    """ An implementation of a Binary Search Tree """
    def __init__(self):
        self.root = None
        
    def count(self, lo, hi):
        ptr = self.root
        i = 0
        n = 0
        while ptr != None and i < hi: 
            if i >= lo:
                n+= 1
            i += 1
        return n

    def add(self, item):
        """ Add this item to its correct position on the tree """
        # This is a non recursive add method. A recursive method would be cleaner.
        if self.root == None: # ... Empty tree ...
            self.root = Node(item, None, None) # ... so, make this the root
        else:
            # Find where to put the item
            child_tree = self.root
            while child_tree != None:
                parent = child_tree
                if item < child_tree.item: # If smaller ... 
                    child_tree = child_tree.left # ... move to the left
                else:
                    child_tree = child_tree.right

            # child_tree should be pointing to the new node, but we've gone too far
            # we need to modify the parent nodes
            if item < parent.item:
                parent.left = Node(item, None, None)
            else:
                parent.right = Node(item, None, None)
    def count_leaves(bst, ptr):
        if ptr.left == None and ptr.right == None:
            return 1
        else:
            count = 0
            if ptr.left != None:
                count += bst.count_leaves(ptr.left)
            if ptr.right != None:
                count += bst.count_leaves(ptr.right)
        return count
    def is_maximal(bst):
        maxHeight = bst.height()
        topLeaves = bst.count_leaves(bst.root)
        if 2**(maxHeight-1) == topLeaves:
            return True
        else:
            return False
    def height(bst):
        return bst.recursive_height(bst.root)              

    def recursive_height(bst, ptr):
        if  ptr == None:
            return 0
        else:
            return 1 + max(bst.recursive_height(ptr.left), bst.recursive_height(ptr.right))
           
def balanced(new_lst, lst):
    if len(lst) == 0:
    	return 
    else:
    	mid = len(lst)//2
    	new_lst.append(lst[mid])
    	balanced(new_lst, lst[:mid])
    	balanced(new_lst, lst[mid+1:])
    	return new_lst	
def make_list(lst):
    lst = sorted(lst)
    new_lst = []
    return balanced(new_lst, lst)

def main():
    bt = BST()
    lst = [10,7,15,5,9,13,20]
    newlst = make_list(lst)
    for i in newlst:
        bt.add(i)
    
if __name__ == "__main__":
    main()
