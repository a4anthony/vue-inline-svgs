<script>
class Svg {
  constructor(path) {
    const div = document.createElement('div')
    div.innerHTML = path
    // change to wherever your svg files are
    const fragment = document.createDocumentFragment()
    fragment.appendChild(div)
    this.svg = fragment.querySelector('svg')
  }
  classes(classes) {
    if (classes) {
      this.svg.classList = ''
      classes.split(' ').forEach((className) => {
        this.svg.classList.add(className)
      })
    }
    return this
  }
  width(width) {
    if (width) {
      this.svg.setAttribute('width', width)
    }
    return this
  }

  fill(fill) {
    if (fill) {
      this.svg.setAttribute('fill', fill)
    }
    return this
  }

  height(height) {
    if (height) {
      this.svg.setAttribute('height', height)
    }
    return this
  }
  toString() {
    return this.svg.outerHTML
  }
}

import { h } from 'vue'

export default {
  props: {
    path: { type: String, required: true },
    classes: {
      type: String,
      default: '',
    },
    fill: {
      type: String,
      default: '',
    },
    size: {
      type: Number,
      default: 15,
    },
    width: {
      type: Number,
      default: null,
    },
    height: {
      type: Number,
      default: null,
    },
  },
  render() {
    return h('div', {
      classList: 'flex-items-center',
      innerHTML: `<span>${new Svg(this.path)
        .classes(this.classes)
        .width(this.width ? this.width : this.size)
        .fill(this.fill)
        .height(this.height ? this.height : this.size)}</span>`,
    })
  },
}
</script>
