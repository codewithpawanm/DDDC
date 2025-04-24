import multiprocessing
import time
def shared_memory_task(shared_data):
 for _ in range(5):
  print(f"Shared Data: {shared_data.value}")
 time.sleep(1)
if __name__ == "__main__":
 # Create a shared memory object
 shared_data = multiprocessing.Value('i', 0) # Integer shared memory
 # Create a process that will use the shared memory
 process = multiprocessing.Process(target=shared_memory_task, args=(shared_data,))
 process.start()
 # Modify the shared memory from the main process
 for i in range(5):
  shared_data.value += 1
  print(f"Main Process: {shared_data.value}")
 time.sleep(1)
 process.join()
