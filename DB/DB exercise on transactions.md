Questions
1. A,B,C before log (PS)
2. A,B,C crash time (BUFFER and PS)
3. transactions in undone and redone lists
4. operations in undone and redone lists in order
5. A, B, C after restart (BUFFER and PS)
## Undo-Redo Protocol
Also called "NoForce", because the buffer is not forced to flush.
Here, the buffer manager is quite free to flush dirty pages whenever it wants, so it is not always possible to know the content of the PS.
Remember however that the checkpoint force-flush all the dirty pages that are before the checkpoint (end checkpoint is useless here).
How to choose undo and redo list for transactions?
1. UNDO
	1. means that there is a trace but no commit
	2. it is important for atomicity
	3. it will be scanned backwards
2. REDO
	1. means that the transaction has been committed
	2. it is important for durability
	3. it will be scanned forwards
During restart, Undo and Redo are executed in the buffer, meaning that they may or may not have been flushed into PS.

## No-Undo Protocol
Also called "Pin Policy".
It means that every transaction is pinned and cannot be flushed until the pin is released with the commit. Basically, the buffer manager is limited by pins. Therefore, there is no risk of flushing uncommitted transactions, meaning that undo is not necessary.
Of course, committed transactions are unpinned and therefore they may or may not be flushed, because the buffer manager is still free to decide when to flush unpinned pages. For this reason, the Redo list is still necessary.
What about the checkpoint? If a page is pinned, it cannot be flushed even during the force-flush of the checkpoint. 


## No-Redo Protocol
Also called "Force Protocol".
Here, nothing is pinned. Every transaction is force-flushed before commit to avoid the need of Redo of committed transactions. 
This gives more space for the buffer manager.
It is very convenient for a fast restart, but if there are many updates during runtime, continuously flushing might slow down the system.

![[DB-ex-transactions.pdf#page=1]]
![[DB-ex-transactions.pdf#page=2]]
![[DB-ex-transactions.pdf#page=3]]
![[DB-ex-transactions.pdf#page=4]]



