import serial
import time
ser = serial.Serial(0,9600)
print(ser.name)

#while(True):
#	command=input("Serial input: ")
#	print(command)
#	command=command+"\n"
#	command=command.encode()
#	ser.write(command)

print("Project 4: IDK")
#command="song1"
#command=command+"\n"
#command=command.encode()
#ser.write(command) #telling arduino to play song1

def strPrint(word):
	for x in word:
		print(x)
		time.sleep(0.1)

#strPrint("I WANT CHICKEN")

musicBox=True

while(musicBox):
	print("1: Mortal Kombat")
	print("2: Guile Theme")
	print("3: Exit")
	command=input("Song Input: ")
	print("Song Chosen: "+command)
	print()
	if (command=="3"):
		musicBox=False
	command=command+"\n"
	command=command.encode()
	ser.write(command)

ser.close()
