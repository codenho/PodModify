[1mName[0m
    [1mPod::Modifier[0m - Add sections to an existing POD dynamically.

[1mSYNOPSYS[0m
    Usage :

    use Pod::Modifier;

    # To get full path to current module

    my $pkg = ref(__PACKAGE__);

    $pkg =~ s/::/\//g;

    $pkg .= ".pm";

    my $pkg_fp = $INC{$pkg};

    # Create modifier object

    my $modifier = Pod::Modifier->new(PACKAGE=>"$pkg_fp");

    # Add a section 'OPTIONS' to the Pod of current file,

    # defined in list of files having paths in array @bases. to be indexed in
    output at

    # index '6', and aliased as 'GLOBAL OPTIONS'

    $modifier->addSection(SECTION=>"OPTIONS",SECTION_INDEX=>6,BASE=>\@bases,AL
    IAS=>"GLOBAL OPTIONS");

    # To print on pager, returns undef in this case.

    # Pager used is less, with -R option, Parser used is Pod::Perldoc::ToTerm

    # To use own pod parser and pager, use without PAGE argument, and process
    the returned Pod string.

    $modifier->updatePod(PAGE=>1);

    # To return as string

    my $pod_string = $modifier->updatePod();

  [1mAPIs[0m
   [1mnew (PACKAGE=[0m"/path/to/CurrentPackage.pm")>
    Class constructor.

   [1maddSection ( BASE =[0m SCALAR|ARRAYREF
    SECTION  => SCALAR 
    SECTION_INDEX => SCALAR
    ALIAS => SCALAR (optional) )
    Interface to add a section 'SECTION', defined in file(s) given by 'BASE',
    at index 'SECTION_INDEX', renamed in current Pod as 'ALIAS'.

   [1mupdatePod(PAGE =[0m (0|1))>
    Update and return the modified POD string, which can be parsed using Pod
    parser of choice.

  [1mARGUMENTS[0m
   [1mnew[0m(PACKAGE=>'$package')
    "PACKAGE =>" [4mbase[0m
        SCALAR Path to the current file, to (the Pod of) which additinal
        sections are to be added.

   [1maddSection[0m()
    "BASE =>" [4mbase[0m
        SCALAR The full path to perl module containing section to be added.
        Or, ARRAYREF list of full paths of perl modules containing required
        section.

    "SECTION =>" [4msection[0m
        SCALAR Name of the head (1) section.

    "SECTION_INDEX =>" [4mindex[0m
        SCALAR Attribute to set position of insertion for this section.

    "ALIAS =>" [4malias[0m
        For multiple files, that is, where BASE is array reference, an alias
        can be used to rename the combined sections, using ALIAS.

   [1mupdatePod[0m(PAGE=>0|1)
    "PAGE =>" [4m0|1[0m
        SCALAR Without an argument, or for PAGE=>0, the function will return
        the Pod as a string which can be parsed by parser of choice. For
        PAGE=>1, '/bin/less' is used for paging and Pod::Perldoc::ToTerm for
        parsing. The output is, thus, immediately paged to STDOUT in this
        case.

[1mCAVEATS[0m
    While paging directly using this module, it is assumed the pager 'less' is
    available in system, which is then used with the -R option for constant
    repainting of terminal/ std output. For proper cross platform
    compatibility it is advised not to use this module for paging. Assumption
    is made that sections in modules would be starting as =head(n) and ending
    with =head(n) of the next section, or EOF, whichever first.

[1mSUPPORT[0m
    This module is managed in a GitHub repository,
    <https://github.com/codenho/PodModify> Feel free to fork and contribute,
    or to clone and send patches!

    Please use <https://github.com/codenho/PodModify/issues/new> to file a bug
    report.

    More general questions or discussion about POD should be sent to the
    "pod-people@perl.org" mail list. Send an empty email to
    "pod-people-subscribe@perl.org" to subscribe.

[1mAUTHOR[0m
    Udhav Verma <vermaudh@cpan.org>

[1mLICENSE[0m
    Pod::Usage (the distribution) is licensed under the same terms as Perl.

[1mACKNOWLEDGMENTS[0m
    Bincy Sarah Thomas, for feedback and help in writing this module.

[1mSEE ALSO[0m
    Pod::Usage, Pod::Perldoc, Pod::Select

