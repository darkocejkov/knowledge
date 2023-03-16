# Algorithm for Matrix Chains

```python
matrixchain( p ):
		n = p.length - 1
    let m[1..n][1..n] be new array
    let s[1..n-1][2..n] be new array
        
    for( i = 1 --> n ):
		    m[i][i] = 0
        
    for( L = 2 --> n ):
        for( i = L --> (n-L)+1 ):
		        j = i + L - 1
            m[i][j] = inf
            for( k = i --> (j-1) ):
				        q = m[i][k] + m[k+1][j] + p(i-1)*p(k)*p(j)
                if( q < m[i][j] ):
			              m[i][j] = q
		                s[i][j] = k
                        	
		return m, s
```