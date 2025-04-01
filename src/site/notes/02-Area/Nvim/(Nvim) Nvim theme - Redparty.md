---
{"dg-publish":true,"permalink":"/02-Area/Nvim/(Nvim) Nvim theme - Redparty/","tags":["Area/Nvim"],"noteIcon":"","created":"2025-03-01T22:57:00.000+09:00","updated":"2025-04-01T22:58:33.446+09:00"}
---

빨간색을 좋아하는 사람이 만든 빨강빨강 테마.

## 사용법

1. colors 폴더(대개 `~/.config/nvim/colors`이다. 없으면 생성)에 lua 파일 하나 생성
2. 아래 내용 붙이기
3. nvim 내에서 `:colorscheme redparty(파일 이름)` 실행
4. 맘에 들면 `init.lua`에서 `vim.cmd("colorscheme redparty")` 작성하기

```lua
-- My Custom Neovim Colorscheme
local mytheme = {}

-- 색상 테이블 정의
mytheme.colors = {
    bg = "#220501",     -- 배경색 (Dark)
    fg = "#d84e4b",     -- 기본 글씨색
    red = "#b62e25",    -- 강조 색상 (Red)
    green = "#b94239",
    yellow = "#d95d5b",
    blue = "#d84e4b",
    magenta = "#cc6966",
    cyan = "#e09da4",
    white = "#ffffff",
    comment = "#7c7c7c", -- 주석 색상
}

-- 하이라이트 그룹 설정
function mytheme.set_highlights()
    local hl = vim.api.nvim_set_hl
    local c = mytheme.colors

    -- 기본 스타일 적용
    hl(0, "Normal", { fg = c.fg, bg = c.bg })
    hl(0, "Comment", { fg = c.comment, italic = true })
    hl(0, "String", { fg = c.green })
    hl(0, "Function", { fg = c.blue, bold = true })
    hl(0, "Keyword", { fg = c.red, bold = true })
    hl(0, "Type", { fg = c.yellow })
    hl(0, "Constant", { fg = c.magenta })
    hl(0, "Identifier", { fg = c.cyan })
    hl(0, "Error", { fg = c.white, bg = c.red, bold = true })
end

-- Colorscheme 적용
function mytheme.setup()
    mytheme.set_highlights()
end

-- Colorscheme 로드
mytheme.setup()

return mytheme
```

![](https://i.imgur.com/j6LXkc2.jpeg)
이런 색상이 됩니다