---
title: atom风格配置
date: 2018年11月15日15:33:51
categories:
- 软件
- atom
tags:
- atom
---

根据自己喜欢的风格配置atom.

### 代码如下

```css
/*
 * Your Stylesheet
 *
 * This stylesheet is loaded when Atom starts up and is reloaded automatically
 * when it is changed.
 *
 * If you are unfamiliar with LESS, you can read more about it here:
 * http://www.lesscss.org
 */

@custom-font-family: 'MonacoYahei', 'Roboto', 'Lucida Grande', 'Segoe UI', Ubuntu, Cantarell, sans-serif;
@setting-view-font-family: 'Lucida Grande', 'Segoe UI', Ubuntu, Cantarell, sans-serif;

@highlight: #80CBC4;

// 自定义，为了使 tree view 更加的紧凑
.tree-view {
  font-family: @custom-font-family;
  font-size: 1.00rem;

  li:not(.list-nested-item), li.list-nested-item > .list-item {
    line-height: 1.80rem; // Edit me for height
  }
  .list-group .selected::before, .list-tree .selected::before {
    height: 1.80rem; // Edit me for height
  }
  .name.icon::before {
    margin: 0 0.5rem 0 0;
  }
  .list-tree.has-collapsable-children .list-nested-item > .list-tree > li,
  .list-tree.has-collapsable-children .list-nested-item > .list-group > li {
    padding-left: 1rem;
  }
  .list-tree.has-collapsable-children li.list-item {
    margin-left: 1.3rem;
  }
  .list-tree.has-collapsable-children .list-nested-item > .list-item::before {
    margin-right: 0.3rem;
  }
  .list-tree > li.list-item:hover {
    color: #ffffff;
  }
  .list-tree > .list-nested-item {
    .icon-file-directory {
      &:hover {
        &::before {
          color: #ffffff;
        }
      }
    }
  }

  .list-tree > .list-nested-item.expanded {
    > .header {
      color: #80CBC4;
    }
  }

  .list-tree > li.list-item.selected {
    color: @highlight;
    &:hover {
      color: @highlight;
    }
  }
}

.editor {
}
atom-text-editor {
  // color: white;
  // background-color: hsl(180, 24%, 12%);
    font-family:  "MonacoYahei","Monaco","msyh";
    font-size: 1.20rem;
}
.editor .cursor {

}

.settings-view {
  font-family: @setting-view-font-family;
}

#linter-inline a.eslint {
  color: #000000;
}

atom-workspace {
  atom-pane-container {
    atom-pane {
      .tab-bar {
        .tab {
          max-width: 160px;

          .title {
            font-family: @custom-font-family;
            font-size: 1.00rem;
          }
        }
      }
    }
  }
}
```
