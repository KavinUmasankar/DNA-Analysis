# DNA-Analysis
import sys

def filename_to_string(dna_filename):
    inputfile = open(dna_filename)
    
    lines = inputfile.readlines()
    line = ""
    for x in range(0, len(lines) // 4):
        line += lines[x * 4 + 1][:-1]
    inputfile.close()
    return line

if len(sys.argv) < 2:
    print("You must supply a file name as an argument when running this "
          "program.")
    sys.exit(2)
filename = sys.argv[1]
nucleotides = filename_to_string(filename)

a = 0
t = 0
c = 0
g = 0
gc = 0
at = 0
for x in range(0, len(nucleotides) - 1):
    if nucleotides[x] == "A":
        a += 1
        at += 1
    if nucleotides[x] == "T":
        t += 1
        at += 1
    if nucleotides[x] == "C":
        c += 1
        gc += 1
    if nucleotides[x] == "G":
        g += 1
        gc += 1
print("GC-content: " + str(gc / (c+g+a+t)))
print("AT-content: " + str(at / (c+g+a+t)))
print("G count: " + str(g))
print("C count: " + str(c))
print("A count: " + str(a))
print("T count: " + str(t))
print("Sum of G+C+A+T counts :" + str(c+g+a+t))
print("Total count: " + str(len(nucleotides)))
print("Length of nucleotides: " + str(len(nucleotides)))
print("AT/GC Ratio " + str(at/gc))
if (gc/(c+g+a+t)) >= 0.6:
    print("GC classification: high GC content")
elif (gc/(c+g+a+t)) <= 0.4:
    print("GC classification: low GC content")
else:
    print("GC classificatoin: moderate GC content")
