# Interactive-3-Dimensional-Gibbs-Free-Energy-landscape-plot-from-MD-simulation-results
### Introduction:
#### A system's potential states are mapped out in an energy landscape. The idea is commonly applied in physics, chemistry, and biochemistry to represent, among other things, all conceivable chemical configurations, the spatial locations of molecules interacting in a system, or parameters and their corresponding energy levels, usually <font color='red'> Gibbs free energy</font>.
> # G = H – TS
> Where, G stands for Gibbs fre energy, H stands for Heat content, T is absolute temperature and S represents entrophy of the system.
> ### *Steps to perform 3-dimensional FEL studies:*
##### 1) Download and keep the Script file <font color=‘red’> “xpm2txt.py” </font> in the present working directory (pwd).
##### 2) Open the bash command line in the pwd: 
##### 3) Type the command :
> <font color=‘green’> python2 xpm2txt.py -f gibbs.xpm -o fel.txt </font>
##### 4) Copy the content of the <font color=‘red’> “fel.txt” </font> in excel and save it as <font color=‘red’> “fel.csv” </font> format.
Python code to plot the graph is given below.

#importin the libraries:
import pandas as pd
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D
from matplotlib import cm

#for the plot to be interactive
%matplotlib notebook  

# Read the CSV file into a dataframe
df = pd.read_csv('file1.csv')

# Extract the required columns from the dataframe
x = df[df.columns[0]]
y = df[df.columns[1]]
z = df[df.columns[2]]

# Create a figure and a 3D axis
fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')

# Create a surface plot with gradient colors (red, yellow, green, blue)
surf = ax.plot_trisurf(x, y, z, cmap='turbo', linewidth=0.2)

# Remove grid lines
ax.grid(False)

# Remove x, y, and z axis values
ax.set_xticklabels([])
ax.set_yticklabels([])
ax.set_zticklabels([])

# Add a color bar to the side for the surface plot
fig.colorbar(surf, shrink=0.5, aspect=5)

# Set labels and title for the plot
ax.set_xlabel('PC1')
ax.set_ylabel('PC2')
ax.set_zlabel('Gibbs Free Energy')

# Create a scatter plot in the xy-plane
ax.scatter(x, y, z.min() - 0.1*(z.max()-z.min()), c=z, cmap='plasma')

# Set limits for the xy-plane
ax.set_zlim(z.min() - 0.1*(z.max()-z.min()), z.max())

# Show the plot
plt.show()
### Save the image1 in higher dpi in the pwd:
plt.savefig('3dimensional_FEL.png', dpi=600, bbox_inches='tight')
## Corresponding 2- dimensional representation :
import pandas as pd
import matplotlib.pyplot as plt

# Read the CSV file into a dataframe
df = pd.read_csv('file1.csv', header=0)  # Assuming the column names are in the first row

# Extract the required columns from the dataframe
x = df.iloc[:, 0]
y = df.iloc[:, 1]
z = df.iloc[:, 2]

# Create a figure and axis
fig, ax = plt.subplots()

# Create a contour plot
contour = ax.tricontourf(x, y, z, cmap='turbo')

# Remove x and y axis values
ax.set_xticklabels([])
ax.set_yticklabels([])

# Set labels and title
ax.set_xlabel('PC1')
ax.set_ylabel('PC2')
ax.set_title('Gibbs Free Energy')

# Add a color bar
cbar = fig.colorbar(contour)

# Show the plot
plt.show()
# Save the image with desired orientation and resolution
plt.savefig('2dimensional_image_FEL.png', dpi=600, bbox_inches='tight')
### find the native form of the protein residing in the energy basins and try to determine the corresponding frames from the simulation trajectory 
