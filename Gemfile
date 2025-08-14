# Gemfile (기존 내용 모두 지우고 이 내용으로 교체)

source "https://rubygems.org" # 젬을 가져올 저장소 주소

# Jekyll Core (최신 안정 버전 사용)
gem "jekyll", "~> 4.3" # GitHub Pages가 Jekyll 4.x를 사용하므로 이 범위를 유지합니다.

# remote_theme을 사용하기 위한 플러그인 (필수)
gem "jekyll-remote-theme", group: :jekyll_plugins

# jekyll-sass-converter 버전 충돌 해결을 위한 명시적 버전 지정
# jekyll-remote-theme 0.4.3은 jekyll-sass-converter <= 3.0.0을 요구합니다.
# 3.0.0 버전이 jekyll 4.x와도 호환되는지 확인해봐야 하지만, 이 충돌을 해결하는 시도입니다.
gem "jekyll-sass-converter", "~> 3.0.0" # 3.0.0 버전을 강제하여 호환성 문제 해결 시도

# _config.yml에 선언된 다른 플러그인들
group :jekyll_plugins do
  gem "jekyll-feed"
  gem "jekyll-seo-tag"
  gem "jekyll-paginate"
  gem "liquid-md5"
  gem "jekyll-tagging"
  gem "kramdown-parser-gfm"
end

# 이전에 설치했던 특정 bundler 버전이 필요한 경우 아래 라인을 사용 (활성화 필요 시)
# gem "bundler", "2.2.34" # `bundle _2.2.34_ install`과 연계