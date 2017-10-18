Parameters were adjusted during the course of a couple of testing loops used to find a reasonable parameter space; at the bottom is the full log of the last loop.

Mappers: no improvements when going above 4, so the best value is 4. 
Reducers: no improvements when going above 8, so the best value is 8.
Memory: lowering it to 256 causes terasort mappers to fail, increasing to 1024 brings no benefit. 512 is thus the best value to use.

Best result:
```
Settings: 4 mappers, 8 reducers, 512 MB container memory, 409 MB mapper heap, 409 MB reducer heap

Running teragen

real	1m10.485s
user	0m6.359s
sys	0m0.282s

Running terasort

real	2m29.447s
user	0m9.041s
sys	0m0.347s
```

Worst result:
```
Settings: 12 mappers, 1 reducers, 1024 MB container memory, 819 MB mapper heap, 819 MB reducer heap

Running teragen

real	1m9.466s
user	0m6.297s
sys	0m0.284s

Running terasort

real	4m37.395s
user	0m9.234s
sys	0m0.371s
```

Full output of the last test run:
```
Testing loop started on Wed Oct 18 12:27:33 UTC 2017

Settings: 4 mappers, 1 reducers, 512 MB container memory, 409 MB mapper heap, 409 MB reducer heap

Running teragen

real	1m11.536s
user	0m6.344s
sys	0m0.285s

Running terasort

real	4m25.202s
user	0m8.985s
sys	0m0.353s

Deleted resourcelabs/tuning/results/tg-10GB-4-1-512
Deleted resourcelabs/tuning/results/ts-10GB-4-1-512

Settings: 4 mappers, 1 reducers, 1024 MB container memory, 819 MB mapper heap, 819 MB reducer heap

Running teragen

real	1m10.609s
user	0m5.893s
sys	0m0.278s

Running terasort

real	4m20.405s
user	0m8.749s
sys	0m0.376s

Deleted resourcelabs/tuning/results/tg-10GB-4-1-1024
Deleted resourcelabs/tuning/results/ts-10GB-4-1-1024

Settings: 4 mappers, 4 reducers, 512 MB container memory, 409 MB mapper heap, 409 MB reducer heap

Running teragen

real	1m10.500s
user	0m6.023s
sys	0m0.260s

Running terasort

real	2m45.632s
user	0m7.847s
sys	0m0.345s

Deleted resourcelabs/tuning/results/tg-10GB-4-4-512
Deleted resourcelabs/tuning/results/ts-10GB-4-4-512

Settings: 4 mappers, 4 reducers, 1024 MB container memory, 819 MB mapper heap, 819 MB reducer heap

Running teragen

real	1m8.533s
user	0m6.441s
sys	0m0.261s

Running terasort

real	2m43.031s
user	0m8.991s
sys	0m0.362s

Deleted resourcelabs/tuning/results/tg-10GB-4-4-1024
Deleted resourcelabs/tuning/results/ts-10GB-4-4-1024

Settings: 4 mappers, 8 reducers, 512 MB container memory, 409 MB mapper heap, 409 MB reducer heap

Running teragen

real	1m10.485s
user	0m6.359s
sys	0m0.282s

Running terasort

real	2m29.447s
user	0m9.041s
sys	0m0.347s

Deleted resourcelabs/tuning/results/tg-10GB-4-8-512
Deleted resourcelabs/tuning/results/ts-10GB-4-8-512

Settings: 4 mappers, 8 reducers, 1024 MB container memory, 819 MB mapper heap, 819 MB reducer heap

Running teragen

real	1m10.544s
user	0m6.473s
sys	0m0.297s

Running terasort

real	2m31.869s
user	0m8.179s
sys	0m0.335s

Deleted resourcelabs/tuning/results/tg-10GB-4-8-1024
Deleted resourcelabs/tuning/results/ts-10GB-4-8-1024

Settings: 8 mappers, 1 reducers, 512 MB container memory, 409 MB mapper heap, 409 MB reducer heap

Running teragen

real	1m10.827s
user	0m6.280s
sys	0m0.289s

Running terasort

real	4m35.622s
user	0m9.079s
sys	0m0.356s

Deleted resourcelabs/tuning/results/tg-10GB-8-1-512
Deleted resourcelabs/tuning/results/ts-10GB-8-1-512

Settings: 8 mappers, 1 reducers, 1024 MB container memory, 819 MB mapper heap, 819 MB reducer heap

Running teragen

real	1m10.624s
user	0m6.399s
sys	0m0.309s

Running terasort

real	4m26.559s
user	0m9.566s
sys	0m0.412s

Deleted resourcelabs/tuning/results/tg-10GB-8-1-1024
Deleted resourcelabs/tuning/results/ts-10GB-8-1-1024

Settings: 8 mappers, 4 reducers, 512 MB container memory, 409 MB mapper heap, 409 MB reducer heap

Running teragen

real	1m4.822s
user	0m6.024s
sys	0m0.278s

Running terasort

real	2m50.326s
user	0m8.852s
sys	0m0.342s

Deleted resourcelabs/tuning/results/tg-10GB-8-4-512
Deleted resourcelabs/tuning/results/ts-10GB-8-4-512

Settings: 8 mappers, 4 reducers, 1024 MB container memory, 819 MB mapper heap, 819 MB reducer heap

Running teragen

real	1m6.674s
user	0m6.106s
sys	0m0.315s

Running terasort

real	2m50.058s
user	0m9.335s
sys	0m0.365s

Deleted resourcelabs/tuning/results/tg-10GB-8-4-1024
Deleted resourcelabs/tuning/results/ts-10GB-8-4-1024

Settings: 8 mappers, 8 reducers, 512 MB container memory, 409 MB mapper heap, 409 MB reducer heap

Running teragen

real	1m12.642s
user	0m6.443s
sys	0m0.324s

Running terasort

real	2m33.783s
user	0m8.589s
sys	0m0.357s

Deleted resourcelabs/tuning/results/tg-10GB-8-8-512
Deleted resourcelabs/tuning/results/ts-10GB-8-8-512

Settings: 8 mappers, 8 reducers, 1024 MB container memory, 819 MB mapper heap, 819 MB reducer heap

Running teragen

real	1m9.617s
user	0m6.080s
sys	0m0.291s

Running terasort

real	2m36.792s
user	0m8.454s
sys	0m0.314s

Deleted resourcelabs/tuning/results/tg-10GB-8-8-1024
Deleted resourcelabs/tuning/results/ts-10GB-8-8-1024

Settings: 12 mappers, 1 reducers, 512 MB container memory, 409 MB mapper heap, 409 MB reducer heap

Running teragen

real	1m7.620s
user	0m5.968s
sys	0m0.248s

Running terasort

real	4m35.781s
user	0m8.995s
sys	0m0.340s

Deleted resourcelabs/tuning/results/tg-10GB-12-1-512
Deleted resourcelabs/tuning/results/ts-10GB-12-1-512

Settings: 12 mappers, 1 reducers, 1024 MB container memory, 819 MB mapper heap, 819 MB reducer heap

Running teragen

real	1m9.466s
user	0m6.297s
sys	0m0.284s

Running terasort

real	4m37.395s
user	0m9.234s
sys	0m0.371s

Deleted resourcelabs/tuning/results/tg-10GB-12-1-1024
Deleted resourcelabs/tuning/results/ts-10GB-12-1-1024

Settings: 12 mappers, 4 reducers, 512 MB container memory, 409 MB mapper heap, 409 MB reducer heap

Running teragen

real	1m10.944s
user	0m6.039s
sys	0m0.271s

Running terasort

real	3m16.408s
user	0m8.804s
sys	0m0.371s

Deleted resourcelabs/tuning/results/tg-10GB-12-4-512
Deleted resourcelabs/tuning/results/ts-10GB-12-4-512

Settings: 12 mappers, 4 reducers, 1024 MB container memory, 819 MB mapper heap, 819 MB reducer heap

Running teragen

real	1m7.652s
user	0m6.030s
sys	0m0.283s

Running terasort

real	3m16.251s
user	0m8.468s
sys	0m0.340s

Deleted resourcelabs/tuning/results/tg-10GB-12-4-1024
Deleted resourcelabs/tuning/results/ts-10GB-12-4-1024

Settings: 12 mappers, 8 reducers, 512 MB container memory, 409 MB mapper heap, 409 MB reducer heap

Running teragen

real	1m10.486s
user	0m6.214s
sys	0m0.295s

Running terasort

real	2m50.663s
user	0m8.238s
sys	0m0.325s

Deleted resourcelabs/tuning/results/tg-10GB-12-8-512
Deleted resourcelabs/tuning/results/ts-10GB-12-8-512

Settings: 12 mappers, 8 reducers, 1024 MB container memory, 819 MB mapper heap, 819 MB reducer heap

Running teragen

real	1m11.989s
user	0m5.961s
sys	0m0.304s

Running terasort

real	2m47.970s
user	0m8.849s
sys	0m0.340s

Deleted resourcelabs/tuning/results/tg-10GB-12-8-1024
Deleted resourcelabs/tuning/results/ts-10GB-12-8-1024

Testing loop ended on Wed Oct 18 13:50:34 UTC 2017
```