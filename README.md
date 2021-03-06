# E57Converter
Convert E57 point cloud format to PCL pcd format 

# Submodules
	Xerces-C (for libE57Format):https://github.com/apache/xerces-c
	libE57Format: https://github.com/asmaloney/libE57Format

# Dependency
	PCL: https://github.com/PointCloudLibrary/pcl

# How to build
	1. clone with submodul: git clone --recursive https://github.com/dogod621/E57Converter.git
	2. build the project: use CMAKE (PS. you may want to set USING_STATIC_XERCES ON)

# How to use
Demo example:<br>
Test E57 Data from https://lasers.leica-geosystems.com/blk360-data-set-downloads

![DEMO](https://user-images.githubusercontent.com/6807005/57923706-9c782f00-78d5-11e9-9bdc-5087cad178ef.jpg)
	
	
	For example: 
		you want to convert a .e57 file to PCL .pcd file
		
		1. Convert .e57 to PCL OutOfCoreOctree: 
			Command:
				E57Converter.exe -convert -src "D:/src.e57" -dst "D:/dst/" -res 5 -min "-100 -100 -100" -max "100 100 100"
		
			Paramerte description:
				-convert:
					specify you are doing a conversion.
				
				-src:
					input file.
					
				-dst
					output file, for this example is a not exist folder ( You must give a not exist folder for create PCL OutOfCoreOctree ).
					
				-res: 
					means node dimension of the octree, for this exammple is 5 meters.
					
				-min: 
					means AABB xyz of octree minimum, for this exammple is -100 meter.
					
				-max: 
					means AABB xyz of octree maximum, for this exammple is 100 meter.
					
				-samplePercent 
					sets the sampling percent for constructing LODs.
					(if not given, default is 0.125.)
					
		2. Convert PCL OutOfCoreOctree to .pcd:
			Command:
				E57Converter.exe -convert -src "D:/dst/" -dst "D:/dst.pcd" -voxelUnit 0.05
				
			Paramerte description:
				-convert:
					specify you are doing a conversion
				
				-src:
					input file, for this example is the PCL OutOfCoreOctree folder.
					
				-dst:
					output file.
					
				-voxelUnit:
					the voxel filter voxel size, for this exammple is 0.05 meter (5 cm)
					(For removing duplicate scan points or for downsampling)

# Useful fuctions:
	1. Print .e57 file tree structure (This is useful for e57 developers):
		Command:
			E57Converter.exe -printE57Format -src "D:/src.e57"
		
		Paramerte description:
			-printE57Format:
				specify you want to print .e57 file tree structure.
				
			-src:
				the .e57 file
				
	2. Convert .pcd file to .ply file: 
		(This is different from PCL tool pcd2ply, this will not output point's scan index and intensity, because PLY file users may not want those values )
		Command:
			E57Converter.exe -convert -src "D:/src.pcd" -dst "D:/dst.ply" -rgb
			
			-convert:
				specify you are doing a conversion
				
			-src:
				input file,.
				
			-dst:
				output file.
				
			-rgb:
				specify output point color.
				
			-camera:
				specify output camera (default false)
			
			-binary:
				specify output as binary (default false)
			
	3. Rebuild PCL OutOfCoreOctree LOD:
		Command:
			E57Converter.exe -buildLOD -src "D:/src/" -samplePercent 0.125
	
		Paramerte description:
			-buildLOD:
				specify you want to rebuild PCL OutOfCoreOctree LOD.
				
			-src:
				the PCL OutOfCoreOctree folder.
				
			-samplePercent 
				sets the sampling percent for constructing LODs.
				
			
	
	
		


