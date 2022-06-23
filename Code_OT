import numpy as np
import matplotlib.pyplot as plt
# NO other imports are allowed

class Shape:
    '''
    DO NOT MODIFY THIS CLASS

    DO NOT ADD ANY NEW METHODS TO THIS CLASS
    '''
    def __init__(self):
        self.T_s = None
        self.T_r = None
        self.T_t = None
    
    
    def translate(self, dx, dy):
        '''
        Polygon and Circle class should use this function to calculate the translation
        '''
        self.T_t = np.array([[1, 0, dx], [0, 1, dy], [0, 0, 1]])
 

    def scale(self, sx, sy):
        '''
        Polygon and Circle class should use this function to calculate the scaling
        '''
        self.T_s = np.array([[sx, 0, 0], [0, sy, 0], [0, 0, 1]])
 
        
    def rotate(self, deg):
        '''
        Polygon and Circle class should use this function to calculate the rotation
        '''
        rad = deg*(np.pi/180)
        self.T_r = np.array([[np.cos(rad), np.sin(rad), 0],[-np.sin(rad), np.cos(rad),0], [0, 0, 1]])

        
    def plot(self, x_dim, y_dim):
        '''
        Polygon and Circle class should use this function while plotting
        x_dim and y_dim should be such that both the figures are visible inside the plot
        '''
        x_dim, y_dim = 1.2*x_dim, 1.2*y_dim
        plt.plot((-x_dim, x_dim),[0,0],'k-')
        plt.plot([0,0],(-y_dim, y_dim),'k-')
        plt.xlim(-x_dim,x_dim)
        plt.ylim(-y_dim,y_dim)
        plt.grid()
        plt.show()



class Polygon(Shape):
    '''
    Object of class Polygon should be created when shape type is 'polygon'
    '''
    def __init__(self, A):
        '''
        Initializations here
        '''
        self.A=np.array(A)
        self.original=np.copy(self.A)#creating a copy for plotting previous state
 
    
    def translate(self, dx, dy=np.inf):
        '''
        Function to translate the polygon
    
        This function takes 2 arguments: dx and dy
    
        This function returns the final coordinates
        '''
        if dy==np.inf:
        #setting default of dy as infinity, so that if parameter not passed it can be reassigned as dx
            dy=dx
        self.original=np.copy(self.A)#updating copy to accomodate updates in self.A(if any)
        Shape.translate(self,dx,dy)
        coordinate=(self.A).transpose()
        translate=self.T_t#calling translate matrix from Shape class
        final=np.matmul(translate,coordinate)
        self.A=final.transpose()
        a,b=[],[]
        for i in range(len(self.A)):
            a.append(self.A[i][0])
            b.append(self.A[i][1])
        return(np.around(np.array(a),2),np.around(np.array(b),2))#rounding off to 2 decimal places
        

    
    def scale(self, sx, sy=np.inf):
        '''
        Function to scale the polygon
    
        This function takes 2 arguments: sx and sx
    
        This function returns the final coordinates
        '''
        if sy==np.inf:
            sy=sx
        self.original=np.copy(self.A)
        Shape.scale(self,sx,sy)
        scale=self.T_s
        xsum,ysum=0,0
        for i in range(len(self.A)):
            xsum+=self.A[i][0]
            ysum+=self.A[i][1]
        xm=xsum/len(self.A)#x coordinate of center of shape
        ym=ysum/len(self.A)#y coordinate of center of shape
        for i in range(len(self.A)):
            self.A[i]=np.dot(scale,[self.A[i][0]-xm,self.A[i][1]-ym,1])#translating by -xm,-ym
        for i in range(len( self.A)):
            self.A[i][0]+=xm
            self.A[i][1]+= ym#translating back by +xm,+ym
        a,b=[],[]
        for i in range(len(self.A)):
            a.append(self.A[i][0])
            b.append(self.A[i][1])
        return(np.around(np.array(a),2),np.around(np.array(b),2))
        
 
    
    def rotate(self, deg, rx = 0, ry = np.inf):
        '''
        Function to rotate the polygon
    
        This function takes 3 arguments: deg, rx(optional), ry(optional). Default rx and ry = 0. (Rotate about origin)
    
        This function returns the final coordinates'''
        if ry==np.inf:
            ry=rx
        Shape.rotate(self,deg)
        rotate=self.T_r
        self.original=np.copy(self.A)
        for i in range(len(self.A)):
            self.A[i]=np.dot(rotate,[self.A[i][0]-rx,self.A[i][1]-ry,1])
        for i in range(len( self.A)):
            self.A[i][0]+=rx
            self.A[i][1]+=ry
        a,b=[],[]
        for i in range(len(self.A)):
            a.append(self.A[i][0])
            b.append(self.A[i][1])
        return(np.around(np.array(a),2),np.around(np.array(b),2))
    
    def plot(self):
        '''
        Function to plot the polygon
    
        This function should plot both the initial and the transformed polygon
    
        This function should use the parent's class plot method as well
    
        This function does not take any input
    
        This function does not return anything
        '''
        a,b=[],[]#creating lists of current x and y coordinate
        for i in range(len(self.A)):
            a.append(self.A[i][0])
            b.append(self.A[i][1])
        a.append(self.A[0][0])    
        b.append(self.A[0][1])
        plt.plot(a,b,color='black')#plots current state
        c,d=[],[]#creating lists of previous x and y coordinate
        for i in range(len(self.original)):
            c.append(self.original[i][0])
            d.append(self.original[i][1])
        c.append(self.original[0][0])    
        d.append(self.original[0][1])
        plt.plot(c,d,color='grey', linestyle='dashed')#plots previous state
        a.extend(c)
        b.extend(d)
        xlimit = max(a,key=abs)#maximum absolute value of x coordinate from both current and previous state
        ylimit = max(b,key=abs)#maximum absolute value of y coordinate from both current and previous state
        Shape.plot(self,xlimit,ylimit)
        


class Circle(Shape):
    '''
    Object of class Circle should be created when shape type is 'circle'
    '''
    def __init__(self, x=0, y=0, radius=5):
        '''
        Initializations here
        '''
        self.x=x
        self.y=y
        self.radius=radius
        
    
    def translate(self, dx, dy=np.inf):
        '''
        Function to translate the circle
    
        This function takes 2 arguments: dx and dy (dy is optional).
    
        This function returns the final coordinates and the radius
        '''
        if dy==np.inf:
            dy=dx
        self.originalx=self.x
        self.originaly=self.y
        self.originalradius=self.radius
        Shape.translate(self,dx,dy)
        coordinate=[[self.x],[self.y],[1.]]#creating matrix(column vector) of x,y and 1.
        translate=self.T_t
        final=np.matmul(translate,coordinate)
        self.x=round(float(final[0][0]),2)#rounding to 2 decimals
        self.y=round(float(final[1][0]),2)
        return self.x,self.y,self.radius
        
        
 
        
    def scale(self, sx):
        '''
        Function to scale the circle
    
        This function takes 1 argument: sx
    
        This function returns the final coordinates and the radius
        '''
        self.originalx=self.x
        self.originaly=self.y
        self.originalradius=self.radius
        Shape.scale(self,sx,sx)
        scale=self.T_s
        self.radius=self.radius*abs(scale[0][0])#multiplying to absolute value of scale
        self.x=round(float(self.x),2)
        self.y=round(float(self.y),2)
        self.radius=round(float(self.radius),2)
        return self.x,self.y,self.radius
 
    
    def rotate(self, deg, rx = 0, ry = np.inf):
        '''
        Function to rotate the circle
    
        This function takes 3 arguments: deg, rx(optional), ry(optional). Default rx and ry = 0. (Rotate about origin)
    
        This function returns the final coordinates and the radius
        '''
        if ry==np.inf:
            ry=rx
        self.originalx=self.x
        self.originaly=self.y
        self.originalradius=self.radius
        Shape.rotate(self,deg)
        coordinate=[[self.x-rx],[self.y-ry],[0]]#shifting by -rx and -ry
        rotate=self.T_r
        final=np.matmul(rotate,coordinate)
        self.x=final[0][0]+rx #shifting back by +rx and +ry
        self.y=final[1][0]+ry
        self.x=round(float(self.x),2)
        self.y=round(float(self.y),2)
        self.radius=round(float(self.radius),2)
        return self.x,self.y,self.radius
 
    
    def plot(self):
        '''
        Function to plot the circle
    
        This function should plot both the initial and the transformed circle
    
        This function should use the parent's class plot method as well
    
        This function does not take any input
    
        This function does not return anything
        '''
        circle= plt.Circle((self.x,self.y),self.radius,fill=False,ls='-')#current state
        axis=plt.gca()
        axis.add_artist(circle)
        originalcircle= plt.Circle((self.originalx,self.originaly),self.originalradius,fill=False,ls='dashed')#previous state
        axis=plt.gca()
        axis.add_artist(originalcircle)
    
        xlimit = max(abs(self.x),abs(self.originalx))+max(self.radius,self.originalradius)
        #sum of maximum absolute value of x coordinate of centers of both states and maximum radius
        ylimit = max(abs(self.y),abs(self.originaly))+max(self.radius,self.originalradius)
        #sum of maximum absolute value of y coordinate of centers of both states and maximum radius
        Shape.plot(self,xlimit,ylimit)

if __name__ == "__main__":
    '''
    Add menu here as mentioned in the sample output section of the assignment document.
    '''
    verbose=int(input('verbose? 1 to plot, 0 otherwise:'))#Taking verbose
    testcases=int(input('Enter the number of test cases:'))#Number of testcases
    for i in range(testcases):
        shape=int(input('Enter type of shape (polygon/circle):'))#choosing the shape
        if shape==1:#circle
            z = list(map(float,input('Enter x-coordinate,y-coordinate and radius (space-separated):').split()))
            x_,y_,radius_=0,0,5 #if len(z)<3 it can take these pre-assigned values
            if len(z)>0:
                x_=z[0]
            if len(z)>1:
                y_=z[1]
            if len(z)>2:
                radius_=z[2]
            crcle=Circle(x_,y_,radius_)
            a_=crcle.scale(1)#for printing original x,y,r
            number=int(input('Enter the number of queries:'))
            print('Enter Query: \n1) R deg (rx) (ry) \n2) T dx (dy) \n3) S sr \n4) P')
            for i in range(number):
                query=input('Enter query and parameters(space seperated):').split()
                if verbose==1:#wants to plot
                    if query[0]=='R':#Rotate
                        print(' '.join(list(map(str,a_))))#printing in one line space separated
                        r_x,r_y=0,0
                        if len(query)>=3:
                            r_x=float(query[2])
                        if len(query)>=4:
                            r_y=float(query[3])
                        a_ =crcle.rotate(float(query[1]),r_x,r_y)   
                        print(' '.join(list(map(str,a_))))
                        crcle.plot()
                        
                    if query[0]=='T':#Translate
                        print(' '.join(list(map(str,a_))))
                        d_x,d_y=float(query[1]),float(query[1])
                        if len(query)==3:
                            d_y=float(query[2])
                            
                        a_=crcle.translate(d_x,d_y)
                        print(' '.join(list(map(str,a_))))
                        crcle.plot()   
                              
                    if query[0]=='S':#Scale
                        print(' '.join(list(map(str,a_))))
                        s_r=float(query[1])
                        a_=crcle.scale(s_r)
                        print(' '.join(list(map(str,a_))))
                        crcle.plot()
                              
                    if query[0]=='P':#Plot
                        crcle.plot()
                              
                elif verbose==0:#only the output
                    if query[0]=='R':
                        print(' '.join(list(map(str,a_))))
                        r_x,r_y=0,0
                        if len(query)>=3:
                            r_x=float(query[2])
                        if len(query)>=4:
                            r_y=float(query[3])
                            
                        a_=crcle.rotate(float(query[1]),r_x,r_y)
                        print(' '.join(list(map(str,a_))))
                        
                    if query[0]=='T':
                        print(' '.join(list(map(str,a_)))) 
                        d_x,d_y=float(query[1]),float(query[1])
                        if len(query)==3:
                            d_y=float(query[2])
                            
                        a_=crcle.translate(d_x,d_y)
                        print(' '.join(list(map(str,a_))))
                              
                    if query[0]=='S':
                        print(' '.join(list(map(str,a_))))
                        s_r=float(query[1])
                        a_=crcle.scale(s_r)
                        print(' '.join(list(map(str,a_))))
                              
                    if query[0]=='P':
                        crcle.plot()
                              
                              
        if shape==0:#polygon
            sides=int(input('Enter the number of sides: '))
            s=[]
            for i in range(sides):
                z = list(map(float,input('Enter(x'+str(i+1)+',y'+str(i+1)+'):').split()))
                z.append(1.)
                s.append(z)
            polygn=Polygon(np.array(s))
            a,b=polygn.scale(1)#for printing original coordinates
            a_=a.tolist()
            b_=b.tolist()
            a_.extend(b_)
            number=int(input('Enter the number of queries:'))
            print('Enter Query: \n1) R deg (rx) (ry) \n2) T dx (dy) \n3) S sx (sy) \n4) P')
            for i in range(number):
                query=input('Enter query and parameters(space seperated):').split()
                if verbose==1:#plot
                    if query[0]=='R':#Rotate
                        print(' '.join(list(map(str,a_))))
                        r_x,r_y=0,0
                        if len(query)>=3:
                            r_x=float(query[2])
                        if len(query)>=4:
                            r_y=float(query[3])
                            
                        a,b=polygn.rotate(float(query[1]),r_x,r_y)
                        a_=a.tolist()
                        b_=b.tolist()
                        a_.extend(b_)
                        print(' '.join(list(map(str,a_))))
                        polygn.plot()
                        
                        
                    if query[0]=='T':#Translate
                        print(' '.join(list(map(str,a_))))
                        d_x,d_y=float(query[1]),float(query[1])
                        if len(query)==3:
                            d_y=float(query[2])
                        a,b=(polygn.translate(d_x,d_y))
                        a_=a.tolist()
                        b_=b.tolist()
                        a_.extend(b_)
                        print(' '.join(list(map(str,a_))))
                        polygn.plot() 
                              
                    if query[0]=='S':#Scale
                        print(' '.join(list(map(str,a_))))
                        s_x,s_y=float(query[1]),float(query[1])
                        if len(query)==3:
                              s_y=float(query[2])
                        a,b=(polygn.scale(s_x,s_y))
                        a_=a.tolist()
                        b_=b.tolist()
                        a_.extend(b_)
                        print(' '.join(list(map(str,a_))))
                        polygn.plot()
                              
                    if query[0]=='P':#Plot
                        polygn.plot()
                    
                              
                elif verbose==0:#print outputs only
                    if query[0]=='R':
                        print(' '.join(list(map(str,a_))))
                        r_x,r_y=0,0
                        if len(query)>=3:
                            r_x=float(query[2])
                        if len(query)>=4:
                            r_y=float(query[3])
                            
                        a,b=polygn.rotate(float(query[1]),r_x,r_y)
                        a_=a.tolist()
                        b_=b.tolist()
                        a_.extend(b_)
                        print(' '.join(list(map(str,a_))))
                        
                        
                    if query[0]=='T':
                        print(' '.join(list(map(str,a_))))
                        d_x,d_y=float(query[1]),float(query[1])
                        if len(query)==3:
                            d_y=float(query[2])
                        a,b=(polygn.translate(d_x,d_y))
                        a_=a.tolist()
                        b_=b.tolist()
                        a_.extend(b_)
                        print(' '.join(list(map(str,a_))))
                         
                              
                    if query[0]=='S':
                        print(' '.join(list(map(str,a_))))
                        s_x,s_y=float(query[1]),float(query[1])
                        if len(query)==3:
                              s_y=float(query[2])
                        a,b=(polygn.scale(s_x,s_y))
                        a_=a.tolist()
                        b_=b.tolist()
                        a_.extend(b_)
                        print(' '.join(list(map(str,a_))))
                        
                              
                    if query[0]=='P':
                        polygn.plot()
