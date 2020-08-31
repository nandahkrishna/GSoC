# GSoC 2020 Report

<p align="center">
  <a href="https://summerofcode.withgoogle.com">
    <img src="assets/GSoC.png" alt="GSoC" width="80" style="margin: 20px">
  </a>
  <a href="https://github.com/Homebrew">
    <img src="assets/Homebrew.png" alt="Homebrew" width="80" style="margin: 20px">
  </a>
</p>

**Author**: [Nanda H Krishna](https://github.com/nandahkrishna)

**Organisation**: [Homebrew](https://github.com/Homebrew)

**Project**: [Adding a livecheck Formula DSL and migrating Livecheckables to homebrew/core](https://github.com/Homebrew/brew/issues/7027)

**Mentors**: [Sam Ford](https://github.com/samford), [Mike McQuaid](https://github.com/MikeMcQuaid), [Sean Molenaar](https://github.com/SMillerDev), [Rui Chen](https://github.com/chenrui333), [Thierry Moisan](https://github.com/Moisan)

## Project Description

Homebrew has a `brew livecheck` command which checks upstream sources (web pages, files, Git repositories) to identify the latest version of software in a formula. `livecheck` uses its built-in strategies to identify versions for certain URLs and this works fine for some formulae. However, it is sometimes necessary to provide explicit information to `livecheck`, telling it where to check and how to identify versions in the fetched content.

Prior to this GSoC project, these `livecheck` instructions were found in the homebrew/livecheck tap's `Livecheckables` folder. "Livecheckable" files were minimal substitutes for formulae and only consisted of a class with `livecheck` information inside. Throughout `livecheck`'s development, there was a desire to eventually incorporate this information into homebrew/core formulae, so the livecheckable files were merely a stopgap measure.

The `livecheck` information was originally formatted as a hash argument to a `livecheck` method. While this format was functional, it didn't follow the existing norms within formulae and would need to be modified. Homebrew uses various domain-specific languages (DSLs) when establishing formula information, so it was necessary to add a `livecheck` DSL to the `Formula` class before the `livecheck` information could be incorporated into homebrew/core formulae.

Adding the `livecheck` DSL and incorporating the livecheckables into homebrew/core formulae were two expressed goals of this GSoC project. The `livecheck` DSL was the first task that was completed and it was implemented early in the project. Due to the ongoing work on livecheckables in the homebrew/livecheck tap, we waited until close to the end of GSoC to migrate the `livecheck` blocks into homebrew/core formulae.

Outside of these initial goals, we also decided to incorporate the `brew livecheck` command into the main Homebrew/brew repository, making it a built-in developer command. Before this point, users were required to tap homebrew/livecheck to be able to use this command.

As a result of this project, the homebrew/livecheck tap is no longer needed and has been deprecated. Further work related to the `brew livecheck` command will happen in Homebrew/brew and work on `livecheck` blocks will happen in homebrew/core formulae.

## Completed Tasks

* Implemented a `livecheck` DSL in Homebrew/brew and incorporated it into the `Formula` class
* Added support for the `livecheck` DSL to the `brew livecheck` command
* Updated existing livecheckables to use the new DSL format
* Removed support for the old livecheckable format from `brew livecheck`
* Added the ability to reference certain formula URLs as `url` symbol arguments (`:head`, `:homepage`, `:stable`)
* Updated livecheckables to use URL symbols, where possible
* Added autocompletion for `brew livecheck`
* Added `url` information to the livecheckables that only contained a regex
* Added livecheckables for some of the formulae that require an explicit check to be able to identify versions
* Updated existing livecheckables to bring them closer to current standards
* Integrated the `livecheck` blocks found in livecheckable files into their respective homebrew/core formulae
* Integrated the `brew livecheck` command into Homebrew/brew as a `dev-cmd`
* Removed all files from the homebrew/livecheck tap and deprecated it

## Ongoing and Future Tasks

* Add RuboCops to enforce standards for `livecheck` block information
* Add/improve network-related `livecheck` tests
* Other improvements to `livecheck`, including adding `livecheck` blocks to formulae, adding a progress bar for JSON output, documentation, etc.

## Challenges and Takeaways

* Before GSoC, I had zero knowledge of Ruby. As an aspiring polyglot (human and programming languages), learning a new language was a fun challenge. Ruby is now one of my favourite languages and I definitely see myself brewing up projects using it.
* Homebrew has a huge codebase, it took quite some time to wrap my head around some of the internals that were central to this project.
* I had other work alongside this project, and one of the biggest challenges was time management. I identified a few strategies that worked for me, and I was able to plan ahead and complete my work efficiently.
* I was able to automate some of the work by writing scripts, something I enjoy doing. With this I was able to identify what tasks could be automated and how, complete them quickly and gain some extra Ruby knowledge.
* My code quality has definitely improved, thanks to detailed reviews from the mentors. I'm working on improving the quality of my documentation and tests.

## Acknowledgements

I'd like to thank my mentors for helping me throughout this project. A special shoutout to my primary mentor Sam for their amazing and comprehensive code reviews and guidance. I enjoyed our weekly meetings and am extremely grateful to them for taking the time to answer all my questions. The Homebrew community is welcoming and friendly, and the maintainers are just brilliant. I'm glad I got an opportunity to work closely with them thanks to GSoC, and I'm looking forward to contributing to Homebrew in the future. I'd also like to acknowledge my wonderful co-GSoCers, [rmNULL](https://github.com/rmNULL) and [Vidushee Amoli](https://github.com/VidusheeAmoli), it was great fun working with them.

## Pull Requests

### [Homebrew/brew](https://github.com/Homebrew/brew)

#### GSoC

* \#7179 - [Livecheck Formula DSL](https://github.com/Homebrew/brew/pull/7179)
* \#7578 - [livecheck: add component order rubocop](https://github.com/Homebrew/brew/pull/7578)
* \#7625 - [livecheck: modified urls cop](https://github.com/Homebrew/brew/pull/7625)
* \#7668 - [livecheck: reference Formula URLs](https://github.com/Homebrew/brew/pull/7668)
* \#7671 - [livecheck: modify regex in tests](https://github.com/Homebrew/brew/pull/7671)
* \#7748 - [Add completion for livecheck](https://github.com/Homebrew/brew/pull/7748)
* \#8180 - [livecheck migration: add `brew livecheck` developer command](https://github.com/Homebrew/brew/pull/8180)
* \#8254 - [livecheck migration: create Homebrew::Livecheck](https://github.com/Homebrew/brew/pull/8254)
* \#8255 - [livecheck migration: add strategies](https://github.com/Homebrew/brew/pull/8255)
* \#8544 - [livecheck: remove test for `livecheck_formulae`](https://github.com/brew/pull/8544)

### [Homebrew/homebrew-core](https://github.com/Homebrew/homebrew-core)

#### Pre-GSoC

* \#40791 - [anime-downloader 3.6.3 (new formula)](https://github.com/Homebrew/homebrew-core/pull/40791)
* \#45722 - [anime-downloader 4.0.1](https://github.com/Homebrew/homebrew-core/pull/45722)

#### GSoC

* \#54565 - [Add livecheck block to a52dec.rb](https://github.com/Homebrew/homebrew-core/pull/54565)
* \#54595 - [aacgain: add livecheck block](https://github.com/Homebrew/homebrew-core/pull/54595)
* \#54597 - [imap-uw: add livecheck block](https://github.com/Homebrew/homebrew-core/pull/54597)
* \#55321 - [detekt: update homepage](https://github.com/Homebrew/homebrew-core/pull/55321)
* \#55950 - [livecheck: modify Formula urls](https://github.com/Homebrew/homebrew-core/pull/55950)
* \#56290 - [ossp-uuid: update homepage](https://github.com/Homebrew/homebrew-core/pull/56290)
* \#57627 - [aacgain: update livecheck regex](https://github.com/Homebrew/homebrew-core/pull/57627)
* \#58760 - [vsts-cli: deprecate](https://github.com/Homebrew/homebrew-core/pull/58760)
* \#60324 - [livecheck: migrate livecheckables to livecheck blocks](https://github.com/Homebrew/homebrew-core/pull/60324)

### [Homebrew/homebrew-livecheck](https://github.com/Homebrew/homebrew-livecheck)

#### Pre-GSoC

* \#235 - [anime-downloader: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/235)
* \#237 - [\[WIP\] Adding livecheckables for formulae](https://github.com/Homebrew/homebrew-livecheck/pull/237)
* \#238 - [aamath: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/238)
* \#239 - [a52dec: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/239)
* \#240 - [aacgain: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/240)
* \#241 - [abuse: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/241)
* \#242 - [aardvark_shell_utils: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/242)
* \#243 - [lrzip: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/243)
* \#247 - [aalib: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/247)

#### GSoC

* \#555 - [Add support for livecheck DSL](https://github.com/Homebrew/homebrew-livecheck/pull/555)
* \#745 - [Update PyPI livecheck urls](https://github.com/Homebrew/homebrew-livecheck/pull/745)
* \#747 - [archey: update url](https://github.com/Homebrew/homebrew-livecheck/pull/747)
* \#748 - [freetds: update url](https://github.com/Homebrew/homebrew-livecheck/pull/748)
* \#749 - [castxml: update url](https://github.com/Homebrew/homebrew-livecheck/pull/749)
* \#750 - [checkbashisms: update url](https://github.com/Homebrew/homebrew-livecheck/pull/750)
* \#751 - [dpkg: update url](https://github.com/Homebrew/homebrew-livecheck/pull/751)
* \#752 - [fakeroot: update url](https://github.com/Homebrew/homebrew-livecheck/pull/752)
* \#753 - [Fix style offenses in livecheck.rb and utils.rb](https://github.com/Homebrew/homebrew-livecheck/pull/753)
* \#762 - [closure-compiler: update url](https://github.com/Homebrew/homebrew-livecheck/pull/762)
* \#764 - [Convert Livecheckables from Hashes to blocks](https://github.com/Homebrew/homebrew-livecheck/pull/764)
* \#766 - [detekt: update url](https://github.com/Homebrew/homebrew-livecheck/pull/766)
* \#767 - [spice-protocol: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/767)
* \#768 - [plzip: update url and regex](https://github.com/Homebrew/homebrew-livecheck/pull/768)
* \#769 - [livecheck: remove support for hash format](https://github.com/Homebrew/homebrew-livecheck/pull/769)
* \#775 - [Fix Livecheck object instantiation](https://github.com/Homebrew/homebrew-livecheck/pull/775)
* \#779 - [anttweakbar: skip livecheck](https://github.com/Homebrew/homebrew-livecheck/pull/779)
* \#786 - [acme: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/786)
* \#787 - [mosquitto: update url and regex](https://github.com/Homebrew/homebrew-livecheck/pull/787)
* \#788 - [gradle: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/788)
* \#789 - [telnet: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/789)
* \#792 - [mysql-client: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/792)
* \#793 - [bash-completion: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/793)
* \#794 - [scala: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/794)
* \#795 - [libmagic: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/795)
* \#796 - [metis: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/796)
* \#798 - [s-lang: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/798)
* \#799 - [popt: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/799)
* \#800 - [libspatialite: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/800)
* \#801 - [openssh: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/801)
* \#802 - [sdl: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/802)
* \#803 - [ldns: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/803)
* \#804 - [mecab: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/804)
* \#818 - [Reference Formula urls in Livecheckables](https://github.com/Homebrew/homebrew-livecheck/pull/818)
* \#820 - [openjdk: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/820)
* \#821 - [arpoison: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/821)
* \#822 - [fltk: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/822)
* \#823 - [md5sha1sum: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/823)
* \#824 - [algol68g: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/824)
* \#825 - [figlet: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/825)
* \#826 - [epstool: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/826)
* \#827 - [texi2html: skip](https://github.com/Homebrew/homebrew-livecheck/pull/827)
* \#828 - [lrzsz: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/828)
* \#829 - [pstree: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/829)
* \#830 - [makedepend: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/830)
* \#831 - [git-crypt: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/831)
* \#832 - [libcaca: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/832)
* \#833 - [sdl_ttf: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/833)
* \#834 - [sdl_mixer: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/834)
* \#835 - [sdl_image: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/835)
* \#836 - [phpmyadmin: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/836)
* \#837 - [nkf: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/837)
* \#838 - [qhull: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/838)
* \#844 - [media-info: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/844)
* \#845 - [testdisk: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/845)
* \#846 - [selenium-server-standalone: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/846)
* \#847 - [cairomm: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/847)
* \#848 - [bzip2: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/848)
* \#849 - [minicom: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/849)
* \#850 - [libelf: add livecheckable to skip](https://github.com/Homebrew/homebrew-livecheck/pull/850)
* \#851 - [mplayer: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/851)
* \#855 - [neo4j: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/855)
* \#856 - [avrdude: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/856)
* \#857 - [libftdi0: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/857)
* \#858 - [libftdi: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/858)
* \#859 - [ossp-uuid: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/859)
* \#861 - [libhid: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/861)
* \#862 - [xpdf: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/862)
* \#863 - [ipcalc: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/863)
* \#864 - [newt: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/864)
* \#865 - [iftop: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/865)
* \#866 - [fcrackzip: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/866)
* \#867 - [lxc: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/867)
* \#868 - [less: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/868)
* \#869 - [oath-toolkit: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/869)
* \#870 - [Add completion for livecheck](https://github.com/Homebrew/homebrew-livecheck/pull/870)
* \#871 - [dependency-check: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/871)
* \#872 - [rethinkdb: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/872)
* \#873 - [libyubikey: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/873)
* \#874 - [pssh: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/874)
* \#875 - [john: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/875)
* \#876 - [notmuch: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/876)
* \#879 - [pyside: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/879)
* \#880 - [tnftp: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/880)
* \#881 - [libspectre: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/881)
* \#882 - [hping: add livecheckable to skip](https://github.com/Homebrew/homebrew-livecheck/pull/882)
* \#883 - [rpm2cpio: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/883)
* \#884 - [pure-ftpd: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/884)
* \#885 - [mit-scheme: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/885)
* \#886 - [corkscrew: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/886)
* \#887 - [cvs: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/887)
* \#888 - [msmtp: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/888)
* \#889 - [desktop-file-utils: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/889)
* \#891 - [smpeg: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/891)
* \#915 - [tcping: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/915)
* \#916 - [ncftp: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/916)
* \#917 - [neon: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/917)
* \#918 - [argp-standalone: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/918)
* \#919 - [mp4v2: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/919)
* \#920 - [markdown: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/920)
* \#921 - [ispell: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/921)
* \#922 - [pidof: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/922)
* \#923 - [clisp: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/923)
* \#924 - [mariadb-connector-c: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/924)
* \#925 - [ucl: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/925)
* \#926 - [juju: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/926)
* \#927 - [cloog: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/927)
* \#928 - [jhead: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/928)
* \#929 - [spidermonkey: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/929)
* \#930 - [sleepwatcher: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/930)
* \#938 - [foremost: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/938)
* \#939 - [swaks: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/939)
* \#940 - [libstfl: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/940)
* \#941 - [sdl_sound: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/941)
* \#942 - [gst-python: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/942)
* \#943 - [megatools: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/943)
* \#944 - [rmtrash: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/944)
* \#945 - [bsdiff: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/945)
* \#946 - [pip-completion: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/946)
* \#947 - [nexus: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/947)
* \#950 - [libotr: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/950)
* \#951 - [pdflib-lite: add livecheckable to skip](https://github.com/Homebrew/homebrew-livecheck/pull/951)
* \#952 - [blast: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/952)
* \#953 - [libsvg: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/953)
* \#954 - [libedit: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/954)
* \#955 - [vsftpd: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/955)
* \#956 - [procmail: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/956)
* \#957 - [superlu: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/957)
* \#958 - [base64: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/958)
* \#959 - [scalapack: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/959)
* \#960 - [eye-d3: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/960)
* \#961 - [rarian: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/961)
* \#962 - [pcsc-lite: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/962)
* \#963 - [grace: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/963)
* \#964 - [minizip: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/964)
* \#965 - [ncview: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/965)
* \#966 - [libsvm: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/966)
* \#967 - [vbindiff: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/967)
* \#968 - [ntp: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/968)
* \#969 - [antiword: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/969)
* \#970 - [sdl_net: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/970)
* \#971 - [ecm: add livecheckable to skip](https://github.com/Homebrew/homebrew-livecheck/pull/971)
* \#972 - [bootloadhid: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/972)
* \#973 - [tcptrace: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/973)
* \#974 - [bcrypt: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/974)
* \#975 - [toilet: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/975)
* \#976 - [most: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/976)
* \#977 - [libsvg-cairo: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/977)
* \#978 - [reaver: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/978)
* \#979 - [lv: add livecheckable to skip](https://github.com/Homebrew/homebrew-livecheck/pull/979)
* \#980 - [opencascade: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/980)
* \#981 - [kim-api: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/981)
* \#982 - [libreplaygain: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/982)
* \#983 - [libcuefile: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/983)
* \#984 - [musepack: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/984)
* \#985 - [ballerina: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/985)
* \#986 - [basex: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/986)
* \#987 - [libagg: add livecheckable to skip](https://github.com/Homebrew/homebrew-livecheck/pull/987)
* \#988 - [asciiquarium: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/988)
* \#989 - [ec2-api-tools: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/989)
* \#990 - [mmv: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/990)
* \#991 - [sloccount: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/991)
* \#992 - [stress: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/992)
* \#993 - [crowdin: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/993)
* \#994 - [hmmer: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/994)
* \#995 - [ifstat: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/995)
* \#996 - [node_exporter: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/996)
* \#997 - [confluent-platform: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/997)
* \#998 - [httperf: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/998)
* \#1000 - [sipcalc: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1000)
* \#1001 - [gst-plugins-bad: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1001)
* \#1002 - [gst-plugins-base: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1002)
* \#1003 - [gst-plugins-good: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1003)
* \#1004 - [gst-plugins-ugly: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1004)
* \#1005 - [gstreamer: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1005)
* \#1006 - [gst-libav: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1006)
* \#1007 - [gst-editing-services: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1007)
* \#1008 - [gst-rtsp-server: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1008)
* \#1009 - [gst-validate: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1009)
* \#1021 - [ttyrec: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1021)
* \#1023 - [dyld-headers: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1023)
* \#1027 - [dns2tcp: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1027)
* \#1028 - [ucspi-tcp: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1028)
* \#1029 - [libestr: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1029)
* \#1030 - [bbftp-client: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1030)
* \#1031 - [wmctrl: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1031)
* \#1032 - [dmg2img: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1032)
* \#1033 - [fastqc: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1033)
* \#1046 - [Add url to Livecheckables](https://github.com/Homebrew/homebrew-livecheck/pull/1046)
* \#1047 - [sdl_gfx: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1047)
* \#1050 - [cadaver: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1050)
* \#1051 - [mockserver: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1051)
* \#1056 - [moarvm: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1056)
* \#1057 - [pwncat: add livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1057)
* \#1061 - [Change `\.j` to `\.jar` in regex](https://github.com/Homebrew/homebrew-livecheck/pull/1061)
* \#1062 - [Change `\.tar` variants to `\.t` in regex](https://github.com/Homebrew/homebrew-livecheck/pull/1062)
* \#1063 - [Change `\.z` to `\.zip` in regex](https://github.com/Homebrew/homebrew-livecheck/pull/1063)
* \#1064 - [bcftools: update url and regex](https://github.com/Homebrew/homebrew-livecheck/pull/1064)
* \#1065 - [byacc: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1065)
* \#1066 - [c-ares: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1066)
* \#1067 - [iozone: update url and regex](https://github.com/Homebrew/homebrew-livecheck/pull/1067)
* \#1068 - [libpst: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1068)
* \#1069 - [libsamplerate: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1069)
* \#1070 - [lua: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1070)
* \#1071 - [lynx: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1071)
* \#1072 - [lzip: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1072)
* \#1073 - [rsync: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1073)
* \#1074 - [siege: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1074)
* \#1075 - [speex: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1075)
* \#1076 - [tokyo-cabinet: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1076)
* \#1077 - [xvid: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1077)
* \#1083 - [Update Livecheckables using GitHub releases page](https://github.com/Homebrew/homebrew-livecheck/pull/1083)
* \#1090 - [wiggle: update url and regex](https://github.com/Homebrew/homebrew-livecheck/pull/1090)
* \#1091 - [mbedtls: update livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1091)
* \#1092 - [python: rename to python@3.8, update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1092)
* \#1124 - [Improve regexes containing `href=.*`](https://github.com/Homebrew/homebrew-livecheck/pull/1124)
* \#1125 - [Improve regexes containing `href=.+` and `href=.+?`](https://github.com/Homebrew/homebrew-livecheck/pull/1125)
* \#1127 - [Change `href=".*` and `href=".*?` to `href=.*?`](https://github.com/Homebrew/homebrew-livecheck/pull/1127)
* \#1128 - [Change `[ '">]` to `["' >]`](https://github.com/Homebrew/homebrew-livecheck/pull/1128)
* \#1141 - [Change `href="` followed by name to `href=.*?`](https://github.com/Homebrew/homebrew-livecheck/pull/1141)
* \#1142 - [Change `href="` followed by version directory to `href=.*?`](https://github.com/Homebrew/homebrew-livecheck/pull/1142)
* \#1143 - [jenkins-lts: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1143)
* \#1144 - [bashdb: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1144)
* \#1145 - [libwps: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1145)
* \#1146 - [remake: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1146)
* \#1147 - [vault: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1147)
* \#1151 - [Change `href="` followed by path to `href=.*?`](https://github.com/Homebrew/homebrew-livecheck/pull/1151)
* \#1152 - [Change `href=".*?/` to `href=.*?`](https://github.com/Homebrew/homebrew-livecheck/pull/1152)
* \#1153 - [Change `url=.+?` to `url=.*?`](https://github.com/Homebrew/homebrew-livecheck/pull/1153)
* \#1154 - [bcpp: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1154)
* \#1155 - [chkrootkit: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1155)
* \#1156 - [daq: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1156)
* \#1157 - [etsh: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1157)
* \#1158 - [exiftool: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1158)
* \#1160 - [fizmo: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1160)
* \#1161 - [fs-uae: update url and regex](https://github.com/Homebrew/homebrew-livecheck/pull/1161)
* \#1162 - [gcc: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1162)
* \#1163 - [ghc: update url and regex](https://github.com/Homebrew/homebrew-livecheck/pull/1163)
* \#1164 - [gwenhywfar: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1164)
* \#1165 - [nss: update url and regex](https://github.com/Homebrew/homebrew-livecheck/pull/1165)
* \#1167 - [Update PyPI urls to stable Formula urls](https://github.com/Homebrew/homebrew-livecheck/pull/1167)
* \#1168 - [opus: update url and regex](https://github.com/Homebrew/homebrew-livecheck/pull/1168)
* \#1169 - [packer: update url and regex](https://github.com/Homebrew/homebrew-livecheck/pull/1169)
* \#1170 - [qrencode: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1170)
* \#1171 - [qtfaststart: update url and regex](https://github.com/Homebrew/homebrew-livecheck/pull/1171)
* \#1172 - [r: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1172)
* \#1173 - [sane-backends: update url and regex](https://github.com/Homebrew/homebrew-livecheck/pull/1173)
* \#1174 - [strongswan: update url and regex](https://github.com/Homebrew/homebrew-livecheck/pull/1174)
* \#1175 - [terraform: update url and regex](https://github.com/Homebrew/homebrew-livecheck/pull/1175)
* \#1176 - [zanata-client: update url and regex](https://github.com/Homebrew/homebrew-livecheck/pull/1176)
* \#1187 - [mbedtls: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1187)
* \#1188 - [Change remaining `href=".*?` to `href=.*?`](https://github.com/Homebrew/homebrew-livecheck/pull/1188)
* \#1189 - [Make Livecheckable regexes case-insensitive](https://github.com/Homebrew/homebrew-livecheck/pull/1189)
* \#1203 - [Update `([0-9.]+)` in regexes](https://github.com/Homebrew/homebrew-livecheck/pull/1203)
* \#1210 - [Update `HREF="` to `href=.*?` in regexes](https://github.com/Homebrew/homebrew-livecheck/pull/1210)
* \#1211 - [Update `([0-9.]+)` to `v?(\d{6,8})` in regexes](https://github.com/Homebrew/homebrew-livecheck/pull/1211)
* \#1212 - [Update `([0-9,.]+)` to `v?(\d+(?:\.\d+)+)` in regexes](https://github.com/Homebrew/homebrew-livecheck/pull/1212)
* \#1213 - [bmake: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1213)
* \#1214 - [Update capture group in versioned regexes](https://github.com/Homebrew/homebrew-livecheck/pull/1214)
* \#1215 - [txr: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1215)
* \#1216 - [diffoscope: remove livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1216)
* \#1217 - [abcmidi: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1217)
* \#1218 - [cppad: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1218)
* \#1219 - [Update multiple `[0-9.]+` to `v?(\d+(?:\.\d+)+)` in regexes](https://github.com/Homebrew/homebrew-livecheck/pull/1219)
* \#1220 - [freetype: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1220)
* \#1222 - [Update regex for postgresql@9.5 and postgresql@9.6](https://github.com/Homebrew/homebrew-livecheck/pull/1222)
* \#1224 - [Update `[0-9.-]` and `[0-9.\-]` in regexes](https://github.com/Homebrew/homebrew-livecheck/pull/1224)
* \#1225 - [dialog: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1225)
* \#1226 - [percona-server: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1226)
* \#1227 - [percona-toolkit: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1227)
* \#1231 - [autossh: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1231)
* \#1232 - [Update regexes containing `a-z` and `0-9`](https://github.com/Homebrew/homebrew-livecheck/pull/1232)
* \#1233 - [jpeg: update url and regex](https://github.com/Homebrew/homebrew-livecheck/pull/1233)
* \#1234 - [openrtsp: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1234)
* \#1235 - [readosm: update regex](https://github.com/Homebrew/homebrew-livecheck/pull/1235)
* \#1236 - [vsts-cli: remove livecheckable](https://github.com/Homebrew/homebrew-livecheck/pull/1236)
* \#1244 - [Update delimiter before `v?` to `[._-]`](https://github.com/Homebrew/homebrew-livecheck/pull/1244)
* \#1246 - [Update delimiter before capturing group to `[._-]` and add `v?`](https://github.com/Homebrew/homebrew-livecheck/pull/1246)
* \#1339 - [Delete Tap files](https://github.com/Homebrew/homebrew-livecheck/pull/1339)
