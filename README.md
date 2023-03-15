# sea-level-predictor-in-python
import pandas as pd
import matplotlib.pyplot as plt
from scipy.stats import linregress

def draw_plot():
  # Read data from file
  df = pd.read_csv('epa-sea-level.csv')
  # Create scatter plot
  plt.scatter(x=df.Year,y=df['CSIRO Adjusted Sea Level'])

  # Create first line of best fit
  line = linregress(x=df.Year, y=df['CSIRO Adjusted Sea Level'])

  # Create second line of best fit
  line2 = linregress(x=df[df['Year'] >= 2000].Year, y=df[df['Year'] >= 2000]['CSIRO Adjusted Sea Level'])

  # Add labels and title
  plt.plot(df.Year,line.intercept + line.slope*df.Year)
  plt.plot(df[df['Year'] >= 2000].Year,line2.intercept + line2.slope*df[df['Year'] >= 2000].Year)
  plt.xlabel('Year')
  plt.ylabel('Sea Level (inches)')
  plt.title('Rise in Sea Level')
  
  # Save plot and return data for testing (DO NOT MODIFY)
  plt.savefig('sea_level_plot.png')
  return plt.gca()
