from PIL import Image
import numpy as np
from pylab import *
import os

class  fingerPrint:
    def __init__(self):
        pass
    
    def  predict_KNN (self,test,train,labels, k_1=1):
            '''
            Predict classification rate using KNN

            Input:
		    train - number of training samples which contain finger prints
			test - test sample containing finger prints
			labels - labels for that data
			K - Number of nearest neighbor 
			
			output:
			key - encoding that belongs to a that finger.
									

			'''
					            
	    
            X_data= train
            y_data = labels
            X_test = test
            
            K = k_1
            
            x=test
            dict_dist = {}
            list_dist=[]
            for j in xrange(X_data.shape[0]):
                dist = np.sum(np.square(x-X_data[j]))
                dict_dist[dist] = j
                list_dist.append(dist)
                   
            list_dist.sort()
            count_1 = 0
            count_2 = 0
            count_3 = 0
            for k1 in xrange(K):
                val = list_dist[k1]
                pos = dict_dist[val]
               
                if y_data[pos] == 1.0:
                    count_1 = count_1+1
                elif y_data[pos] == 2.0:
                    count_2 = count_2+1
                else: 
                    count_3 = count_3+1  

                
            if(count_1>=count_2 and count_1>=count_3):
                key = 1
            elif (count_2>=count_1 and count_2>=count_3):
                key = 2
            else: 
                key = 3
            
            return key


def main():
    f=fingerPrint()
    dir_list = [x[0] for x in os.walk('/home/suhaspillai/FingerPrints')]
    sort_list=[]
    sort_list.insert(0,dir_list[0])
    sort_list.insert(1,dir_list[5])
    sort_list.insert(2,dir_list[1])
    sort_list.insert(3,dir_list[2])
    X_data = np.zeros((30,144,144))
    y_data = np.zeros((30))
    count=0
    for i in xrange(1,len(sort_list)):
        folder_path = sort_list[i]
        for j in xrange(1,11):
            file_path=folder_path+'/'+str(j)+'.bmp'
            pil_im = Image.open(file_path)
            im = np.array(pil_im)
            X_data[count] = im
            y_data[count] = int(i)
            
            count=count+1
          
    path = '/home/suhaspillai/songs'
   
    if os.path.exists(path):
        dir_list=os.listdir(path)

    count=0
    while (True):
        dir_list_fprints = [x[2] for x in os.walk('/home/suhaspillai/FingerPrints/Sequence')]
        
        dir_list_fprints=dir_list_fprints[0]
        dir_list_fprints.sort()
        
        
        if not dir_list_fprints:
            print 'exit'
            break
        
        image_path = '/home/suhaspillai/FingerPrints/Sequence/'+dir_list_fprints[0]
       
        dir_list_fprints.pop()
        X_test=np.array(Image.open(image_path))
        val = f.predict_KNN(X_test,X_data,y_data,1)
        os.remove(image_path)
        if val==1:
             
           
           
            if not os.path.isfile(path+'/'+dir_list[count]):
                
                if os.path.exists(path+'/'+dir_list[count]):
                    path = path +'/'+ dir_list[count]
                    dir_list = os.listdir(path)
                    count=0
            else:
                list_file_1 = [x[2] for x in os.walk(path)]
                list_file=list_file_1[0]
                
                new_path = path +'/'+list_file[count]
                print new_path 
        if val==2:
          
            count=count+1
        
if __name__=="__main__":
    pass
    main()
