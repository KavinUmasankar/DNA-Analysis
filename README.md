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
    
    
    
    # This program reads in DNA sequencer output and computes statistics, such as
    # the GC content.  Run it from the command line like this:
    #   python dna_analysis.py myfile.fastq
    #
    # For teaching purposes, a few more comments than normal have been added in
    # to explain in detail what some Python constructs are doing.

    # The sys module supports reading files, command-line arguments, etc.
    import sys


    # Function to convert the contents of dna_filename into a string of nucleotides
    def filename_to_string(dna_filename):
        """
        dna_filename - the name of a file in expected file format
        Expected file format is: Starting with the second line of the file,
        every fourth line contains nucleotides.
        The function will read in all lines from the file containing nucleotides,
        concatenate them all into a single string, and return that string.
        """

        # YOU DO NOT NEED TO MODIFY THIS FUNCTION.

        # Creates a file object from which data can be read.
        inputfile = open(dna_filename)

        # String containing all nucleotides that have been read from the file so
        # far.
        seq = ""

        # The current line number (= the number of lines read so far).
        linenum = 0

        for line in inputfile:
            linenum = linenum + 1
            # if we are on the 2nd, 6th, 10th line...
            if linenum % 4 == 2:
                # Remove the newline characters from the end of the line
                line = line.rstrip()
                # Concatenate this line to the end of the current string
                seq = seq + line
        # close file
        inputfile.close()
        return seq


    # Function to return GC Classification
    def classify(gc_content):
        """
        gc_content - a number representing the GC content
        Returns a string representing GC Classification. Must return one of
        these: "low", "moderate", or "high"
        """

        if gc_content > 0.6:
            classification = "high"
        elif gc_content < 0.4:
            classification = "low"
        else:
            classification = "moderate"
        
        return classification


    ###########################################################################
    # Main program begins here
    #

    # Check if the user provided an argument
    if len(sys.argv) < 2:
        print("You must supply a file name as an argument when running this "
              "program.")
        sys.exit(2)

    # Save the 1st argument provided by the user, as a string.
    # Note: sys.argv[0] is the name of the program itself (dna_analysis.py)
    filename = sys.argv[1]

    # Open the file and read in all nucleotides into a single string of letters
    nucleotides = filename_to_string(filename)

    ###
    # Compute statistics
    ###

    # YOUR CODE GOES BELOW THIS POINT

    # Total nucleotides seen so far.
    total_count = 0

    # Number of G and C nucleotides seen so far.
    gc_count = 0

    for base in nucleotides:
        total_count = total_count + 1

        if base == 'C' or base == 'G':
            gc_count = gc_count + 1

    gc_content = float(gc_count) / total_count

    print('GC-content:', gc_content)

    # You can add more assertions here to check properties that you think
    # should be true about your results. If the condition listed is false,
    # then the given message will be printed.
    assert total_count == len(nucleotides), "total_count != length of nucleotides"
