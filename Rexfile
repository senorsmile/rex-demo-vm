use Rex -feature => ['0.57'];

use Rex::Commands::Box init_file => "box.yml";

user "root";
password "box";

group demo => map { get_box( $_->{name} )->{ip} }
  grep { $_ eq "rex-demo" } list_boxes;

task init => sub {
  boxes "init";
};

task setup_demo => sub {

  account "rex",
    ensure   => "present",
    password => "rex";

  file "/etc/yum.repos.d/rex.repo",
    source => "files/etc/yum.repos.d/rex.repo",
    owner  => "root",
    group  => "root",
    mode   => 644;

  run "import-rex-gpg-key",
    command => "rpm --import http://rex.linux-files.org/RPM-GPG-KEY-REXIFY-REPO.CENTOS6";

  pkg [ "wget", "rex", "perl-App-cpanminus" ],
    ensure => "latest";

  run "install-term-menu",
    command => "cpanm -n Term::Menu";

  file "/etc/issue",
    source => "files/etc/issue",
    owner  => "root",
    group  => "root",
    mode   => 644;

  file "/home/rex/.bashrc",
    source => "files/bachrc",
    owner  => "rex";


  file [ "/home/rex/examples/lesson_1", "/home/rex/examples/lesson_2" ],
    ensure => "directory",
    owner  => "rex",
    group  => "rex";

  file "/home/rex/examples/lesson_1/Rexfile",
    source => "files/examples/lesson_1/Rexfile",
    owner  => "rex",
    group  => "rex",
    mode   => 644;

  file "/home/rex/lessons.pl",
    source => "files/lessons.pl",
    owner  => "rex",
    group  => "rex",
    mode   => 755;

  file "/home/rex/lessons",
    ensure => "directory",
    owner  => "rex",
    group  => "rex",
    mode   => 755;

  sync_up "files/lessons/", "/home/rex/lessons";

};

