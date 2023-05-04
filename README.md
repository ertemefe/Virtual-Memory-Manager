COMP 304: Operating Systems Project 3: Virtual Memory Manager

Arda Aykan Poyraz - Efe Ertem

Part 1

In our implementation, to obtain the offset of the logical address, we bitwise mask with Offset Mask (1111111111). To get the logical page, we first bitwise mask it with Page Mask (11111111110000000000) then shift it to the right by Offset Bits which is 10. For search_tlb, we go through each entry in the TLB table. For add_to_tlb function, we used a fifo implementation which basically does circular indexing with modular operation. Logical page was searched in the TLB table with search_tlp function with the return value of the physical page. If the value is  equal to -1, TLB miss occurs. Then the logical page is searched in the page table and if the return value is equal to -1 it means a page fault happened. To fix the issue the logical page is found from the backstore bin and the content is loaded into a free page which is located in the main memory. 

Part 2

Same principle applies from the first part. In this part, with PM being smaller than VM, we were asked to implement replacement policies. A flag variable is created in order to conduct the operation with FIFO, if flag is equal to 0, or LRU, if flag is equal to 1. We have modified the MEMORY_SIZE in the given source code to be equal to “physical_page_frame_size x page_size”. 
In the FIFO implementation, we found the virtual memory page which is using the physical memory page “new_free_page” and empty it (change value to -1), to enable the next virtual memory page using (Replaced with new). 
In the LRU implementation we have created an array to store the last accessed times. In the lru_replacement method we first find the least recently used physical memory page which will be used by the next Virtual Memory. Then we find the virtual memory page which is using the physical memory page 'index' and empty it (change value to -1), which will be used by the next virtual memory page (Replaced with new).
