ACID (Atomicity, Consistency, Isolation, Durability)
A: all operations work or not 
C: keep consistent status of system
I: transaction integrity to system
  [wiki](https://en.wikipedia.org/wiki/Isolation_(database_systems))
  read phenomena:
  dirty reads/non-repeatable reads/phantom reads
  Isolation levels (higher level used, possibility of deadlock increased)
  LOWER   Read uncommitted (allow dirty reads)
  =>      Read committed (allow non-repeatable reads) - default
  =>      Repeatable reads (allow phantom reads)
  HIGHER  Serializable
D: make update persistent after commit
