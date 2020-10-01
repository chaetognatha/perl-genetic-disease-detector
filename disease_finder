# /usr/bin/perl

use strict;
use warnings;

my @codes = ();
my @name = ();
my @gene = ();
my @repeats = ();

if (!open(DISEASES, "diseases.txt")) {
	 die "Check input file 1\n";
}

my @disease = <DISEASES>; #read from the diseases.txt file
my $lines = scalar(@disease); #count lines
for (my $i=0;$i<$lines;$i++) { #for every line
	chomp($disease[$i]);
	my @path = split(";", $disease[$i]); #split for each value
#put values inside arrays
push (@codes, $path[0]);
push (@name, $path[1]);
push (@gene, $path[2]);
push (@repeats, $path[3]);
}
my @table = (\@codes, \@name, \@gene, \@repeats); #create two dimensional array


print "Input code;\n";
my $input = <STDIN>;
chomp $input; #this is the disease we are looking for

for (my $i=0;$i<$lines;$i++){ #this goes through all cells looking for the input and prints the second cell in that row
for (my $col=0; $col<$lines; $col++){
	if ("${$table[$i]}[$col]\n" =~ /$input/){
			print "${$table[1]}[$col]\n";
		}}}
print "What file needs to be analyzed?:\n";
my $this_file = <STDIN>;#this is the sequence to be analyzed
chomp $this_file;
if (!open(THISFILE, "$this_file")) {
	 die "Check input file 2\n";
}
my $file = join ("", <THISFILE>); #putting it all in a string
#declaring variables
my @reps = ();
my $longest = 0;
my $ls = 0;
my $cs =0;
my $rstring = 0;
my $rcount =0;

while ($file =~ /((CAG){2,})/g){
	push (@reps, $1); #putting all repeats with at least two CAG in array
}
foreach (@reps){
	pop @reps; #take first element
	$ls = length($_); #measure element
	$cs = length($reps[0]); #measure what is now first element
	if ($ls >= $cs){ #compare and if it is bigger, put that into variable
		$longest = $ls; #this takes length and is numeric
		$rstring = $_; #this takes the repeat in nucleotides
	}
}
while ($rstring =~ /CAG/g){ #count how many times CAG repeats in the longest repeat
	$rcount++;
}
print "Repeat length: $rcount\n";

my $threshold = 0;
for (my $i=0;$i<$lines;$i++){ #make this a sub?
for (my $col=0; $col<$lines; $col++){
	if ("${$table[$i]}[$col]\n" =~ /$input/){
			$threshold = "${$table[3]}[$col]\n"; #extract value of pathogenic nr of repeats
		}}}
if ($rcount >= $threshold){#testing if the sequence contains pathogenic repeats
	print "Pathogenic!\n";
} else {
	print "Normal!\n"
}
