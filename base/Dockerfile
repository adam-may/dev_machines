FROM buildpack-deps:xenial
MAINTAINER Adam May <adammay@gmail.com>

RUN locale-gen en_AU.UTF-8

ENV DEBIAN_FRONTEND noninteractive
ENV LANG en_AU.UTF-8
ENV LC_CTYPE en_AU.UTF-8
ENV LC_ALL en_AU.UTF-8

# Change default server and install dependencies
RUN sed -i "s/http:\/\/archive.ubuntu.com\/ubuntu\//http:\/\/mirror.internode.on.net\/pub\/ubuntu\/ubuntu\//g" /etc/apt/sources.list && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y \
            curl \
            git \
            man \
            tmux \
            vim-nox \
            wget \
            zsh && \
    rm -rf /var/lib/apt/lists/*

# Add custom .gitignore
RUN curl -o ~/.gitconfig https://raw.githubusercontent.com/adam-may/dotfiles/master/git/.gitconfig

# Change the shell to using zsh
RUN chsh -s /bin/zsh root

# Setup zsh, including Oh-My-Zsh
RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true

RUN mv ~/.zshrc ~/.zshrc.old

RUN curl -o ~/.zshrc https://raw.githubusercontent.com/adam-may/dotfiles/master/zsh/.zshrc
RUN curl -o ~/.oh-my-zsh/themes/adammay.zsh-theme https://raw.githubusercontent.com/adam-may/dotfiles/master/zsh/adammay.zsh-theme

# Setup tmux
RUN curl -o ~/.tmux.conf https://raw.githubusercontent.com/adam-may/dotfiles/master/tmux/.tmux.conf

# Setup fonts
RUN git clone https://github.com/powerline/fonts.git ~/fonts
RUN ~/fonts/install.sh

# Setup vim.spf13/com
RUN curl -o ~/.vimrc.before.local https://raw.githubusercontent.com/adam-may/dotfiles/master/vim/.vimrc.before.local
RUN curl -o ~/.vimrc.bundles.local https://raw.githubusercontent.com/adam-may/dotfiles/master/vim/.vimrc.bundles.local
RUN curl -o ~/.vimrc.local https://raw.githubusercontent.com/adam-may/dotfiles/master/vim/.vimrc.local

# Setup spf13-vim
RUN curl http://j.mp/spf13-vim3 -L -o - | sh
RUN vim +BundleInstall +BundleClean +qall!

# Create the directory for our SSH keys
RUN mkdir /root/.ssh

CMD ["/bin/zsh"]

