---
id: 850
title: 'Solution: how to use perl convert XLSX to csv'
date: 2014-06-10T03:33:06+00:00
author: edyliu
layout: post
guid: http://192.168.1.77:8880/?p=850
permalink: /2014-06-solution-how-to-use-perl-convert-xlsx-to-csv/
categories:
  - Howto
---
We need xls2csv and Spreadsheet::ParseXLSX
  
get xls2csv from cpan
  
https://metacpan.org/release/Spreadsheet-ParseXLSX

Make modification on xls2csv
  
`<br />
## add option -t means type. xls or xlsx.<br />
< getopts('x:b:t:c:a:qshvWw:n:f', \%O);
<!--more--></p>
<p>## replace the old Book declare with following:<br />
< my $Book;
< if ($O{'t'})
< {
<       my $Parser = Spreadsheet::ParseXLSX->new;<br />
<       my $Formatter = Spreadsheet::ParseExcel::FmtUnicode->new(Unicode_Map => $SourceCharset);<br />
<       $Book = $Parser->parse($XLS, $Formatter) || die "Can't read spreadsheet!";<br />
< }
< else {
<       $Book = Spreadsheet::ParseExcel::Workbook->Parse($XLS, $Formatter) || die "Can't read spreadsheet!\n";<br />
< }
` 

then you can use following commands to convert xlsx
  
xls2csv -x "formate2007.xlsx" -t xlsx -c "newfomart.csv"