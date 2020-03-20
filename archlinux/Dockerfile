FROM archlinux:latest

ENV LANG en_US.UTF-8
RUN echo 'en_US.UTF-8 UTF-8' > /etc/locale.gen && locale-gen

RUN pacman --noconfirm --needed -Syu \
    && pacman -S --noconfirm base-devel pacman-contrib wget git less htop zsh thefuck neovim terraform ripgrep jq kubectl kubectx fasd fd exa bat \
    && paccache -rfk0

RUN sed 's/# %wheel ALL=(ALL) NOPASSWD: ALL/%wheel ALL=(ALL) NOPASSWD: ALL/g' /etc/sudoers > /etc/sudoers.new \
    && export EDITOR="cp /etc/sudoers.new" \
    && visudo \
    && rm /etc/sudoers.new

RUN useradd -m -g users -G wheel -s /bin/bash hemor

USER hemor

RUN cd ~ \
    && git clone https://aur.archlinux.org/yay.git \
    && cd yay \
    && makepkg -si --noconfirm \
    && cd ~ && rm -rf yay

RUN yay -Syu --noconfirm terragrunt-bin aws-cli-v2 k9s kubernetes-helm starship-bin saml2aws-bin \
    && paccache -rfk0

RUN cd ~ && wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true