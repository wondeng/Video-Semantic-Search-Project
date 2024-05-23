Video Semantic Search
Objective
Video makers often require short clips of footage to fill in spaces in the overall video–this rolling footage, known as B-roll, often includes footage of scenery or action relating to the narrative.  At Acts2 Network, we often have large video projects that require extensive amounts of B-roll.  The process of searching for relevant B-roll that matches the mood, content, and narrative of the video is done manually and takes a significant amount of time.

The purpose of this project is to create a library for searching a database of videos for the ones most semantically relevant to an input query.

We aim to use OpenAI's CLIP (Contrastive Language-Image Pretraining), a library designed to understand the relationship between images and text.  Notably, CLIP understands not only image content e.g. “there is a dog”, but also semantic information about the image e.g. “the dog is looking forward to going on a walk”.

By extending CLIP from images to videos, we hope to create a library for video makers to quickly find relevant B-roll and reduce the time required to complete large video projects.
Approach
Video Frame Analysis
Determine an efficient method for selecting frames from each video, as analyzing every frame is too costly.
Use CLIP to generate embeddings (numerical representations of an image’s semantic information) for each frame.
Efficient Embedding Search
Develop an efficient algorithm to search a large number of embeddings to find the most relevant videos based on a given query.
Investigate indexing techniques such as KD-trees, Locality-Sensitive Hashing (LSH), or approximate nearest neighbor (ANN), etc.
Develop a backend and API to retrieve the relevant videos.
Skills You Can Learn

Version Control with Git and GitHub
Agile Development Practices
Image and Video Processing
Machine Learning / AI
Efficient Algorithms and Data Structures
API Design and Development
Testing and Quality Assurance
Documentation and Communication

