# S3 Lifecycle Rules
Whenever i found lifecyle rules the first thing pops up my mind is that moving objects from point A to B. I have thousands of users and their images in my S3. Except their profile picture, i do not need to excess their 
driving license or insurance card picture frequently. So, i decided that after 30 days from the images will move from standard to IA, then IA to Glacier Flexible Retrieval. That's it 
# S3 Storage classes Name
1. Standard - frequent access
2. Standard-IA - Infrequent but quick access
3. One Zone-IA - Infrequent, one AZ only
4. Glacier Flexible Retrieval - Archival, can wait minutes/hours
5. Glacier Deep Archive - 	Archival, long-term (12 hours wait)
6. Intelligent-Tiering - Auto switch based on usage

## AWS S3 storage cost
1. Standard - 1 TB of data - 1024*0.023 = 23.55
2. Standar-IA - 1024*0.0125 = 12.80
3. Glacier - 1024*0.004 = 4.10
4. Deep Archive - 1024 *  0.00099 = $1.01
