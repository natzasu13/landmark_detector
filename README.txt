# Run
D:\TESIS_MAESTERIA\CODIGOS_DE_EJEMPLO\Python\landmark_detector> python .\example_Dlib_webcam.py







# Download the dlib predictor that has been used in the project from : 
http://dlib.net/files/shape_predictor_68_face_landmarks.dat.bz2

Most of the code and the general idea is taken from the link given below:
van Gent, P. (2016). Emotion Recognition Using Facial Landmarks, Python, DLib and OpenCV. A tech blog about fun things with Python and embedded electronics. Retrieved from: http://www.paulvangent.com/2016/08/05/emotion-recognition-using-facial-landmarks/


# Installing and building the required libraries
I am on Windows, and building libraries on Windows always gives many people a bad taste in their mouths. I can understand why, however it’s not all bad and often the problems people run into are either solved by correctly setting PATH variables, providing the right compiler or reading the error messages and installing the right dependencies. I will walk you through the process of compiling and installing Dlib.
First install CMake. This should be straightforward, download the windows installer and install. Make sure to select the option “Add CMake to the system PATH” during the install. Choose whether you want this for all users or just for your account.
Download Boost-Python and extract the package. I extracted it into C:\boost but it can be anything. Fire up a command prompt and navigate to the directory. Then do:
bootstrap.bat #First run the bootstrap.bat file supplied with boost-python
#Once it finished invoke the install process of boost-python like this:
b2 install #This can take a while, go get a coffee
#Once this finishes, build the python modules like this
b2 -a --with-python address-model=64 toolset=msvc runtime-link=static #Again, this takes a while, reward yourself and get another coffee.
Copy~

Once all is done you will find a folder named bin, or bin.v2, or something like this in your boost folder. Now it’s time to build Dlib.
Download Dlib and extract it somewhere. I used C:\Dlib but you can do it anywhere. Go back to your command prompt, or open a new one if you closed it, and navigate to your Dlib folder. Do this sequentially:
# Set two flags so that the CMake compiler knows where to find the boost-python libraries
set BOOST_ROOT=C:\boost #Make sure to set this to the path you extracted boost-python to!
set BOOST_LIBRARYDIR=C:\boost\stage\lib #Same as above
# Create and navigate into a directory to build into
mkdir build
cd build
# Build the dlib tools
cmake ..
#Navigate up one level and run the python setup program
cd ..
python setup.py install #This takes some time as well. GO GET ANOTHER COFFEE TIGER!
Copy~
Open your Python interpreter and type “import dlib”. If you receive no messages, you’re good to go! Nice.

# Testing the landmark detector
Before diving into much of the coding (which probably won’t be much because we’ll be recycling), let’s test the DLib installation on your webcam. For this you can use the following snippet. If you want to learn how this works, be sure to also compare it with the first script under “Detecting your face on the webcam” in the previous post. Much of the same OpenCV code to talk to your webcam, process the image by converting to grayscale, optimising the contrast with an adaptive histogram equalisation and displaying it is something we did there.
