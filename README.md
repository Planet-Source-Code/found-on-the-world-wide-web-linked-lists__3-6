<div align="center">

## Linked Lists


</div>

### Description

This program illustrates many linked list functions. It shows how to create and manage doubly link lists. It is my most advanced DLL program.
 
### More Info
 
A quick note: Some functions may not work with some compilers e.g. clrscr() and getch(). The lines of code which contain these functions may be deleted or commented out without significant change to program functionality. The reason this error occurs is because various compiliers have different functions built in. Your compiler should have corresponding functions which may replace the conflicting or invalid ones. I wrote the code on this page using Borlands Turbo C/C++ ver 3.0 for DOS.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Found on the World Wide Web](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/found-on-the-world-wide-web.md)
**Level**          |Unknown
**User Rating**    |4.0 (12 globes from 3 users)
**Compatibility**  |C
**Category**       |[Miscellaneous](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/miscellaneous__3-1.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/found-on-the-world-wide-web-linked-lists__3-6/archive/master.zip)





### Source Code

```
//Jeff Letendre
#include <stdlib.h>						//for malloc()
#include <stdio.h>						//for printf(), scanf(), fflush()
void main (void);				  		///////////////////////////////////////
struct node * merge (struct node *, struct node *);	   	///////////////////////////////////////
struct node * reverse (struct node **);				///////////////////////////////////////
struct node * createList (void);				///////////////////////////////////////
struct node * subtract (struct node *, struct node *);	  	///////////////////////////////////////
struct node * addSort(int, struct node **);			///////////////////////////////////////
struct node * getMemory(void);					///////////////////////////////////////
struct node * InsertAfter (struct node **);			////////////// prototype //////////////
struct node * intersection (struct node *, struct node *); 	////////////// section //////////////
struct node * search (int, struct node *);			///////////////////////////////////////
struct node * bubbleSort (struct node *);          	///////////////////////////////////////
void PrintList (struct node *);					///////////////////////////////////////
void deleteNode (struct node **);				///////////////////////////////////////
void free_node (struct node **);				///////////////////////////////////////
int palindrome (struct node *plist);				///////////////////////////////////////
void errorExit (char *);					///////////////////////////////////////
struct node							//structure template
  {
  struct node *previous;					//pointer to previous node in list
  int data;							//integer list data
  struct node *next;						//pointer to next node in the list
  };
////////////END OF HEADER SECTION////////////////
void main (void)
  {
  struct node *plist = NULL;				 	//pointer for first list
  struct node *plist2 = NULL;					//pointer for second list
  struct node *pnode = NULL;			  		//pointer for node
  struct node *tempList = NULL;          		//misc. pointer for returned lists
  int option = 0, choice = 0;           		//variables for user input
  while (true)							//main program loop set to infinite loop
   {
   printf("\n\nPlease make a selection:\n\n");		//prompt for input
   printf(" 0 = Add in sorted order\n");
   printf(" 1 = Create a list\n");
   printf(" 2 = Seek and destroy\n");
   printf(" 3 = Exit\n");
   printf(" 4 = Search\n");
   printf(" 5 = Intersection\n");
   printf(" 6 = Print\n");
   printf(" 7 = Merge two lists\n");
   printf(" 8 = Create another list\n");
   printf(" 9 = Palindrome?\n");
   printf("10 = Reverse list \n");
   printf("11 = Subtract two lists\n");
   printf("12 = Insert after\n");
   fflush(stdin);						//clear input buffer
   scanf("%d", &option);            		//scan new option
   switch(option)
     {
     case 0:
	  {
	  printf("Enter an integer to be added to the list or -99999\n");
      scanf("%d", &choice);
	  while (choice != -99999)			   	//call addSort
        {
	    plist = addSort(choice, &plist);
	    printf("Enter another integer or -99999 to quit\n");
	    fflush(stdin);
	    scanf ("%d", &choice);
	    }
      break;
      }
     case 1:
 	  {
      plist = createList();
	  break;
 	  }
     case 2:
	  {
	  deleteNode(&plist);	//no return modifying original list
 	  break;
	  }
     case 3:
 	  {
	  exit(1);
 	  break;
 	  }
     case 4:
	  {
	  printf("Enter a value to search the list for:\n");
	  scanf("%d", &choice);
      tempList = search(choice, plist);
      if (tempList == NULL)
        {
        printf("The value %d was not found in the list\n", choice);
        break;
        }
	  else
        {
        if(tempList->previous == NULL && tempList->next == NULL)
         printf("%d is the only value in the list\n", tempList->data);
        else if(tempList->previous == NULL && tempList->next != NULL)
         printf("%d is the first value in the list followed by %d\n",
           tempList->data, (tempList->next)->data);
        else if(tempList->previous != NULL && tempList->next == NULL)
         printf("%d comes after %d and is the last value in the list\n",
           tempList->data, (tempList->previous)->data);
        else if(tempList->previous != NULL && tempList->next != NULL)
         printf("%d comes after %d and before %dlist\n", tempList->data,
           (tempList->previous)->data, (tempList->next)->data);
        break;
        }
	  }
     case 5:
	  {
      tempList = intersection (plist, plist2);
      if(tempList != NULL)
        {
        tempList = bubbleSort(tempList);
        PrintList(tempList);
        }
	  break;
	  }
     case 6:
	  {
	  PrintList(plist);
	  break;
	  }
     case 7:
      {
   	  tempList = merge (plist, plist2);
      PrintList(tempList);
	  break;
	  }
     case 8:
	  {
	  plist2 = createList();
	  break;
	  }
     case 9:
	  {
	  if(palindrome(plist))				   //if palindrome returns 1
	    {
	    PrintList(plist);
	    printf(" it is a palindrome.\n");
	    }
	  else
        {
	    PrintList(plist);				     //else list is not a palindrome
	    printf(" it is not a palindrome.\n");
	    }
	  break;
	  }
     case 10:
	  {
      PrintList(plist);           //print list before reversing
      printf("\n\nReversing...\n\n");
	  plist = reverse(&plist);			   //call to reverse func
      PrintList(plist);           //print reversed list
	  break;
	  }
     case 11:
	  {
	  printf("How shall I subtract your lists?\n");
      printf("1 = First list entered minus second list entered or\n");
      printf("2 = Second list entered minus first list entered?\n");
      scanf("%d", &choice);
	  if (choice == 1)
        {
        tempList = subtract (plist, plist2);
        }
      else if (choice == 2)
        {
        tempList = subtract (plist2, plist);
        }
      else
        {
        printf("Incorrect choice escaping to main menu\n");
        break;
        }
      PrintList(tempList);
      break;
	  }
     case 12:
	  {
	  plist = InsertAfter(&plist);	//Insert After has capability to
	  break;               //start a new list if plist is empty
	  }
     default:
	  {
	  printf("Your only options are zero (0) through eleven (11)\n");
	  printf("Enter new option\n\n");
	  break;
	  }
     }  //end switch
   }  //end while
  }//////////////end main()/////////////////
struct node * addSort(int newVal, struct node **plist)
  {
  struct node *newNode;
  struct node *ptemp;
  ptemp = *plist;
  newNode = getMemory();			//call getMemory to allocate and test
  newNode->data = newVal;			//copy int into struct
  while(ptemp != NULL && ptemp->data <= newNode->data && ptemp->next != NULL)
   ptemp = ptemp->next;
  if(ptemp == NULL)				//if list is empty
   {
   newNode->next = NULL;			//set next to NULL
   newNode->previous = NULL;		   	//set previous to NULL
   *plist = newNode;				//set list pointer to newNode
   }
  else if(ptemp->previous == NULL && ptemp->data > newNode->data)//at begining of list
   {
   newNode->previous = ptemp->previous;
   newNode->next = ptemp;
   ptemp->previous = newNode;
   *plist = newNode;
   }
  else if(ptemp->next == NULL)		 	//at end of list
   {
   newNode->previous = ptemp;
   newNode->next = ptemp->next;
   ptemp->next = newNode;
   }
  else if(ptemp->data > newNode->data)		//inbetween begining and end of list
   {
   newNode->next = ptemp;
   newNode->previous = ptemp->previous;
   (ptemp->previous)->next = newNode;
   ptemp->previous = newNode;
   }
  return(*plist);				//pass back list pointer
  }	////////////end add sort//////////////////
struct node * bubbleSort (struct node *listHead)//sorts a doubly linked list of ints
  {                      //returns pointer to sorted list
  struct node * listp1 = NULL;
  struct node * listp2 = NULL;
  listp1 = listHead;              //assign pointer to list head
  listp2 = listHead->next;           //assign pointer to next node
  while(listp1 != NULL && listp2 != NULL)
   {
   if(listp1->data <= listp2->data)     //if in ascending order w/ next node
     {
     listp2 = listp2->next;         //skip to next 2 nodes
     listp1 = listp1->next;
     }
   else                   //else swap order
     {
     listp1->next = listp2->next;
     listp2->previous = listp1->previous;
     if(listp1->previous != NULL)      //if not the first node
      (listp1->previous)->next = listp2; //point previous node's next field to listp2
     listp1->previous = listp2;
     if(listp2->next != NULL)        //if there is a next node
      (listp2->next)->previous = listp1; //point its previous field to listp1
     listp2->next = listp1;
     if(listp1 == listHead)         //reset pointers to begining of
      listHead = listp2;
     listp1 = listHead;
     listp2 = listp1->next;
     }
   }  //end while
  return listHead;
  }///////////////////end bubbleSort///////////////////////
struct node * createList(void)
  {
  struct node * plist = NULL;			//pointer for new list
  struct node * temp = NULL;			//pointer for inserting into list
  struct node * pinsert = NULL;		//pointer for node allocation
  pinsert = getMemory();			//call getMemory to allocate and test
  pinsert->next = NULL;			//set node pointers to NULL
  pinsert->previous = NULL;
  plist = pinsert;				//point list pointer to first node
  printf("Type a list of integers to be created\n");
  printf("Enter -99999 to finish input cycle\n");
  printf("Enter first integer for new list\n");
  scanf("%d", &(pinsert->data));	  	//scan new value
  while (pinsert->data != -99999)
   {
   temp = pinsert;
   pinsert = getMemory();			//call getMemory to allocate and test
   pinsert->next = NULL;			//copy NULL to new node's next field
   pinsert->previous = temp;
   temp->next = pinsert;
   printf("Enter an integer to be added after %d:\n", temp->data);
   scanf("%d", &(pinsert->data));		//scan into struct's data element value
   }
  fflush(stdin);
  free(pinsert);				//free node which contains sentinel (-99999)
  temp->next = NULL;              //assign last node's next pointer to NULL
  return (plist);				//returns NULL if list contains sentinel only
  } //////////////End createList/////////////
void deleteNode (struct node ** plist)     //deletes node from list
  {
  struct node *temp = NULL;
  struct node *next1 = NULL;
  int delVal = 0;
  next1 = *plist;				//set pointer to list head
  printf("Enter a value and I will delete all nodes\n");
  printf("whose data element matches your value\n");
  scanf("%d", &delVal);
  while(next1 != NULL)				//search through whole list
   {
   if(next1->data == delVal)			//if delVal is found
     {
	 if(next1->next == NULL && next1->previous == NULL)	//if deleting only node
	  {				   	//deleting only node. Point plist to NULL
	  free(next1);
	  *plist = NULL;
	  }
	 else if(next1->previous == NULL)	//if deleting first node
      {
	  next1 = next1->next;		//skip next1 to next node
	  next1->previous = NULL;		//since first node assign previous to NULL
	  *plist = next1;			//point the list pointer to the new first node
      free(temp);				//free old first node
 	  temp = *plist;			//point temp to list
	  }
     else if(next1->next == NULL)		//if deleting last node
      {
	  temp->next = NULL;			//set temp as last node
	  free(next1);			//free last node in list
	  next1 = temp->next;			//point next1 to NULL;
	  }                  //end else
     else                  //else deleting a node between nodes
      {
	  temp->next = next1->next;		//shift pointer to skip over node to be deleted
	  (next1->next)->previous = temp;	//point previous element of 1st node after deleted node to temp
	  free(next1);			//free node
	  next1 = temp->next;			//point next1 to next node
      }  //end else
     }  //end if
   else
     {
	 temp = next1;
	 next1 = next1->next;			//go through list
	 }                   //end else
   }                   	//end while
  }////////////////end deleteNode()///////////////
void errorExit(char *string)          //prints error & exits program
  {
  printf("%s", &string);
  exit(1);
  }/////////////end errorExit()///////////////
void free_node (struct node **pnode)
  {
  struct node *ptemp;				//temp pointer used for swaping structure pointers
  if(pnode == NULL)				//if list is empty
   errorExit("Attempt to delete from a NULL node pointer");
  ptemp == (*pnode)->previous;		   	//point to previous node
  ptemp->next = (*pnode)->next;		//mend break in links
  free(pnode);					//release memory back to OS
  }/////////end free_node/////////
struct node * getMemory(void)          //allocates & tests return value
  {
  struct node * newPtr = NULL;
  if((newPtr = (struct node *) malloc(sizeof(struct node))) == NULL)
   {  					//if malloc returns a NULL pointer
   printf("ERROR! Unable to allocate memory - Abort\n");
   abort();					//print error msg & abort function
   return(0);				//make the compiler happy :>)
   }
  else
   return newPtr;
  }   ///////////////////end getMemory///////////////
struct node * InsertAfter(struct node **plist)
  {
  struct node *tempNode;
  struct node *tempList;
  int afterVal = 0, choice = 0;
  tempList = *plist;
  tempNode = getMemory();			//call getMemory to allocate and test
  if (tempList == NULL)			//if list is empty
   {
   printf("Your list is empty. Should I create a list for you?\n");
   printf("1 = Yes\n2 = No\n");
   scanf("%d", &choice);
   if(choice == 1)
     {
     printf("Enter an integer\n");     //prompt and get input
     while(scanf("%d", &choice) < 1)    //testing scanf//reusing choice for data input
      printf("Incorrect value entered. Please try again:\n");
     tempNode->data = choice;
     tempNode->previous = NULL;       //set pointers
     tempNode->next = NULL;
     }
   else if(choice == 2)           //if user doesn't want to create list
     tempNode = NULL;            //set return pointer to NULL
   return tempNode;             //return pointer
   }  //end if
  else                 	//list is not empty
   {
   printf("Enter an integer to insert the next node after\n");
   scanf("%d", &afterVal);				//assign new value to data field
   for(; tempList != NULL && tempList->data != afterVal; tempList = tempList->next);
     if (tempList == NULL)
      {
      printf("Error list value not found\n");	//print error msg.
      return(tempList);				//return NULL pointer
	  }
	 else if(tempList->data == afterVal)
      {
	  printf("Enter an integer to be added after %d\n", tempList->data);
	  scanf("%d", &(tempNode->data));		//get new data value
	  tempNode->next = tempList->next;		//assign new node's next field to plist's next field
	  tempList->next = tempNode;		  	//copy temp into plist's next field
	  tempNode->previous = tempList;		//copy plist to temp's previous field
      }
	  }  //end else
	return (*plist);
  }///////////End InsertAfter////////////
struct node * intersection (struct node *opList1, struct node *opList2)
  {
  struct node *temp = NULL;
  struct node *intList = NULL;
  temp = getMemory();
  intList = temp;               	//list head pointer
  if(opList1 == NULL || opList2 == NULL)
   {
   printf("Empty list(s) - can not take intersection\n");
   temp = NULL;
   return temp;
   }
  while (opList1 != NULL)
   {
   if(search(opList1->data, opList2) != NULL)
     {                   	//if data is not in list
     temp->previous = opList1->previous;  	//copy node into new list
	 temp->data = opList1->data;
	 temp->next = getMemory();       	//allocate more memory
     (temp->next)->previous = temp;     	//point next nodes previous field to current node
     temp = temp->next;           	//point temp to next node
     opList1 = opList1->next;
     }  //end if
   else
     opList1 = opList1->next;
   }  //end while
  (temp->previous)->next = NULL;        	//terminate links w/ NULL
  free(temp);                 	//release extra node back to OS
  return intList;
  } /////////////end intersection////////////////
struct node * merge (struct node *listA, struct node *listB)
  {
  struct node * listHead = NULL;      		//pointer to new merged list
  listHead = listA;              		//set pointers to begining of listA
  while (listA->next != NULL)        		//skip to end of listA
   listA = listA->next;
  listB->previous = listA;       		//append listA with listB
  listA->next = listB;
  listHead = bubbleSort(listHead);       	//sort new list
  return listHead;               	//return pointer to new merged sorted list
  } ////////////end merge//////////////////
int palindrome (struct node *plist)
  {
  struct node *temp1;
  struct node *temp2;
  int i = 0, j = 0;
  temp1 = temp2 = plist;					//set both temp vars to the list pointer
  for (i=0; temp2->next != NULL; temp2 = temp2->next, i++);	//terminated for loop to move to end of list
   for(j = 0; j < i; j++)
     {
     if (temp1->data != temp2->data)			//if values not equal
 	  return (0);
	 else
      {
	  temp1 = temp1->next;				//increment temp1
	  temp2 = temp2->previous;				//decrement temp2
      }
     }  //end for loop
  return(1);
  } ///////////end palendrome///////////////
void PrintList (struct node *plist)
  {
  int i = 0;
  if(plist != NULL)
   {
   printf("Here is your list:");
   while (plist != NULL)
     {
	 if((i % 10) == 0)		       	//CRLF first line then print ten values per line
	 printf("\n");
	 printf("--> %d ", plist->data);
	 plist = plist->next;	         	//point plist to next node
	 i++;
	 }  //end while loop
   }  //end else statement
  } ///////////////end PrintList()////////////////
struct node * reverse (struct node ** plist)
  {
  struct node *rList = NULL;
  struct node *ptemp = NULL;
  struct node *pt2 = NULL;
  ptemp = *plist;
  while(ptemp->next != NULL)
   {
   ptemp = ptemp->next;		    		//point ptemp to end of list
   }
  rList = ptemp;
  *plist = rList;				  	//set list pointer to end of list
  while(ptemp != NULL)
   {
   ptemp = ptemp->previous;
   rList->previous = rList->next;
   rList->next = ptemp;
   rList = ptemp;
   }
  return(*plist);
  } //////////end reverse////////////////////
struct node * search (int data, struct node *pstack)
  {
  struct node *ptemp;
  for (ptemp=pstack; ptemp != NULL && ptemp->data != data; ptemp = ptemp->next);
  return ptemp;                	//returns NULL if data not found
  }///////////end of search///////////////
struct node * subtract (struct node *opList1, struct node *opList2)
  {
  struct node *temp = NULL;
  struct node *subList = NULL;
  temp = getMemory();
  subList = temp;               	//list head pointer
  while (opList1 != NULL)
   {
   if(search(opList1->data, opList2) == NULL)
     {                   	//if data is not in list
     temp->previous = opList1->previous;  	//copy node into new list
	 temp->data = opList1->data;
	 temp->next = getMemory();       	//allocate more memory
     (temp->next)->previous = temp;     	//point next nodes previous field to current node
     temp = temp->next;           	//point temp to next node
	 opList1 = opList1->next;
     }                   	//end if
   else
     opList1 = opList1->next;
   }                     	//end while
  (temp->previous)->next = NULL;        	//terminate links w/ NULL
  free(temp);                 	//release extra node back to OS
  return subList;
  }//////////end subtract////////////////
/////////////////////////////////// END PROGRAM /////////////////////////////
```

