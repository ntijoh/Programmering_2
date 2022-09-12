require 'bundler'
Bundler.require

task default: %w[write]

task :write do
  sh 'rerun'
end

task :build do
  sh 'asciidoctor -D docs --backend=html5 -o index.html -a toc2 docs/index.adoc'
end

task :publish do
  sh 'git checkout main'
  Rake::Task["build"].execute
  sh 'git status'
  puts "Add/Commit files? (Y/n) "
  if STDIN.gets.chomp.downcase != 'n'
    puts 'git commit message: '
    msg = STDIN.gets.chomp
    sh 'git add .'
    sh "git commit -m '#{msg}'"
    sh 'git checkout gh-pages'
    sh 'git merge main'
    sh 'git checkout main'
    sh 'git push --all'
  end

end