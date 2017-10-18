```bash
#!/bin/sh
# Confirm the path values given below correspond to your installation

MR=/opt/cloudera/parcels/CDH/lib/hadoop-0.20-mapreduce
HADOOP=/opt/cloudera/parcels/CDH/bin

# Mark start of the loop
echo "Testing loop started on `date`"

# Mapper containers
for i in 4 8 12
do
   # Reducer containers
   for j in 1 4 8
   do                 
      # Container memory
      for k in 512 1024
      do                         
         # Set mapper JVM heap 
         MAP_MB=`echo "($k*0.8)/1" | bc` 

         # Set reducer JVM heap 
         RED_MB=`echo "($k*0.8)/1" | bc` 

         echo -e "\nSettings: $i mappers, $j reducers, $k MB container memory, $MAP_MB MB mapper heap, $RED_MB MB reducer heap\n"

         echo "Running teragen"

         time ${HADOOP}/hadoop jar ${MR}/hadoop-examples.jar teragen \
            -Dmapreduce.job.maps=$i \
            -Dmapreduce.map.memory.mb=$k \
            -Dmapreduce.map.java.opts.max.heap=$MAP_MB \
            100000000 resourcelabs/tuning/results/tg-10GB-${i}-${j}-${k} 1>tera_${i}_${j}_${k}.out 2>tera_${i}_${j}_${k}.err                       

         echo -e "\nRunning terasort"

         time ${HADOOP}/hadoop jar $MR/hadoop-examples.jar terasort \
            -Dmapreduce.job.maps=$i \
            -Dmapreduce.job.reduces=$j \
            -Dmapreduce.map.memory.mb=$k \
            -Dmapreduce.map.java.opts.max.heap=$MAP_MB \
            -Dmapreduce.reduce.memory.mb=$k \
            -Dmapreduce.reduce.java.opts.max.heap=$RED_MB \
	    resourcelabs/tuning/results/tg-10GB-${i}-${j}-${k}  \
            resourcelabs/tuning/results/ts-10GB-${i}-${j}-${k} 1>>tera_${i}_${j}_${k}.out 2>>tera_${i}_${j}_${k}.err                         
	 
         # lazy newline for pretty output
         echo
         $HADOOP/hadoop fs -rm -r -skipTrash resourcelabs/tuning/results/tg-10GB-${i}-${j}-${k}                         
         $HADOOP/hadoop fs -rm -r -skipTrash resourcelabs/tuning/results/ts-10GB-${i}-${j}-${k}                 
      done
   done
done

echo -e "\nTesting loop ended on `date`"
```