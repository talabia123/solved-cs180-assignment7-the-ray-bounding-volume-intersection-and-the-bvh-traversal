Download Link: https://assignmentchef.com/product/solved-cs180-assignment7-the-ray-bounding-volume-intersection-and-the-bvh-traversal
<br>
In the previous assignment, we implemented the basic functionality of ray tracing, namely ray-casting and ray-triangle intersection. To find an intersection between a ray and the scene, we looped over all the objects in the scene and tested if there was an intersection. This works fine when the scene contains a small number of objects. However, when we want to render a complex scene with a huge amount of objects, this naive approach will be very inefficient. This is why we need some acceleration structures to speed up our ray-intersection routine. There are several acceleration structures to use, in this class we focus on the bounding volume hierarchy(BVH), which is an object partition method. In this assignment you will implement the ray-bounding volume intersection and the BVH traversal.

The functions you should take from your previous assignment are:

<ul>

 <li>Render() in cpp: Paste your ray generation code from last assignment here.</li>

 <li>rayTriangleIntersect() in hpp: Paste your ray-triangle intersection function from the last assignment here.</li>

</ul>

The functions you need to implement for this homework: • IntersectP(const Ray&amp; ray, const Vector3f&amp; invDir, const std::array&lt;int, 3&gt;&amp; dirIsNeg) in the Bounds3.hpp: This function implements the bounding box-ray intersection, and by implementing the process in lecture slides, you can find if a ray is intersects with the current bounding box or not.

<ul>

 <li>getIntersection(BVHBuildNode* node, const Ray ray)in cpp: After constructing the BVH, we can use it to accelerate our intersection routine. This is a recursive function and you need to call the Bounds3::IntersectP function you finished here.</li>

</ul>

<h1>1           Getting started</h1>

The only dependency of the start code is CMake. It should be able to run on your own machine. Please download the project’s skeleton code, and build the project by using the following commands:

1 mkdir build 2 cd ./build 3 cmake .. 4 make

After this, you should be able to run the given code by using ./Raytracing. There are several updates of the code base. Some general introductions are:

<ul>

 <li>hpp: We separate the material parameters of an object to a class, now each object instance holds their own material.</li>

 <li>hpp: This is the structure contains the information of an intersection.</li>

 <li>hpp: The ray class, contains its origin, direction, transport time t and its range.</li>

 <li>hpp: The class for our axis-aligned bounding box. Each bounding box can be specified by two points, pMin and pMax (why?). The Bounds3::Union function combines two bounding boxes into a new one. Also, each object in the scene holds their own bounding box.</li>

 <li>hpp: The class of our BVH acceleration structure. The scene now holds a BVHAccel instance. And start from a root node, we can recursively build our BVH from the objects list of the scene. The BVH is indeed a binary tree of the BVHBuildNode struct.</li>

</ul>