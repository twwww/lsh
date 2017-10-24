# lsh

This program implements a Locality-Sensitive Hashing method for near-duplicate detection in the MapReduce setting.

The input for mapper is in the form (key, value), where the key is None and the value is the shingles of one page. We generate hash functions to hash to shingles in the page and take the lowest value for each function. This procedure is equivalent to generating a random permutation of all possible shingles. After this step we get a MinHash signatures. Then, we split the matrix into b bands with r rows and record the band id and signatures values, which is reprsented by a variable called 'bucket'. In the mapper we finally output page id and 'bucket'.

For the reducer, the input is an aggregation of the ouput of the mapper. If any of the bucket of two pages are exactly the same, we classify them as candidate pair and output them.

