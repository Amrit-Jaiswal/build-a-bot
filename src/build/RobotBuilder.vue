<template>
  <div>
    <div class="top-row">
      <div class="robot-name">{{selectedRobot.head.title}}</div>
      <div class="top part">
        <!-- <img src="./images/head-big-eye.png" title="head" /> -->
        <img v-bind:src="selectedRobot.head.src" title="head" />
        <button v-on:click="selectPrevHead()" class="prev-selector">&#9668;</button>
        <button v-on:click="selectNextHead()" class="next-selector">&#9658;</button>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img v-bind:src="availableParts.arms[selectLeftArmIndex].src" title="left arm" />
        <button v-on:click="selectPrevLeftArm()" class="prev-selector">&#9650;</button>
        <button v-on:click="selectNextLeftArm()" class="next-selector">&#9660;</button>
      </div>
      <div class="center part">
        <img v-bind:src="availableParts.torsos[selectTorsos].src" title="left arm" />
        <button v-on:click="selectPrevTorsos()" class="prev-selector">&#9668;</button>
        <button v-on:click="selectNextTorsos()" class="next-selector">&#9658;</button>
      </div>
      <div class="right part">
        <img v-bind:src="availableParts.arms[selectRightArmIndex].src" title="left arm" />
        <button v-on:click="selectPrevRightArm()" class="prev-selector">&#9650;</button>
        <button v-on:click="selectNextRightArm()" class="next-selector">&#9660;</button>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img v-bind:src="availableParts.bases[selectBaseIndex].src" title="left arm" />
        <button v-on:click="selectPrevBase()" class="prev-selector">&#9668;</button>
        <button v-on:click="selectNextBase()" class="next-selector">&#9658;</button>
      </div>
    </div>
  </div>
</template>
<script>
import availableParts from "../data/parts";

function getPrevValidIndex(index, length) {
  const decrementedIndex = index - 1;
  return decrementedIndex < 0 ? length - 1 : decrementedIndex;
}

function getNextValidIndex(index, length) {
  const incrementedIndex = index + 1;
  return incrementedIndex > length - 1 ? 0 : incrementedIndex;
}

export default {
  name: "RobotBuilder",
  data() {
    return {
      availableParts,
      selectHeadIndex: 0,
      selectLeftArmIndex: 0,
      selectRightArmIndex: 0,
      selectTorsos: 0,
      selectBaseIndex: 0
    };
  },
  computed: {
    selectedRobot() {
      return {
        head: availableParts.heads[this.selectHeadIndex],
        leftArm: availableParts.arms[this.selectLeftArmIndex],
        rightArm: availableParts.arms[this.selectRightArmIndex],
        torso: availableParts.torsos[this.selectTorsos],
        base: availableParts.bases[this.selectBaseIndex]
      };
    }
  },
  methods: {
    selectNextHead() {
      this.selectHeadIndex = getNextValidIndex(
        this.selectHeadIndex,
        this.availableParts.heads.length
      );
    },
    selectPrevHead() {
      this.selectHeadIndex = getPrevValidIndex(
        this.selectHeadIndex,
        this.availableParts.heads.length
      );
    },
    selectPrevLeftArm() {
      this.selectLeftArmIndex = getPrevValidIndex(
        this.selectLeftArmIndex,
        this.availableParts.arms.length
      );
    },
    selectNextLeftArm() {
      this.selectLeftArmIndex = getNextValidIndex(
        this.selectLeftArmIndex,
        this.availableParts.arms.length
      );
    },
    selectPrevRightArm() {
      this.selectRightArmIndex = getPrevValidIndex(
        this.selectRightArmIndex,
        this.availableParts.arms.length
      );
    },
    selectNextRightArm() {
      this.selectRightArmIndex = getNextValidIndex(
        this.selectRightArmIndex,
        this.availableParts.arms.length
      );
    },
    selectPrevTorsos() {
      this.selectTorsos = getPrevValidIndex(
        this.selectTorsos,
        this.availableParts.torsos.length
      );
    },
    selectNextTorsos() {
      this.selectTorsos = getNextValidIndex(
        this.selectTorsos,
        this.availableParts.torsos.length
      );
    },
    selectPrevBase() {
      this.selectBaseIndex = getPrevValidIndex(
        this.selectBaseIndex,
        this.availableParts.torsos.length
      );
    },
    selectNextBase() {
      this.selectBaseIndex = getNextValidIndex(
        this.selectBaseIndex,
        this.availableParts.torsos.length
      );
    }
  }
};
</script>

<style>
.part {
  position: relative;
  width: 165px;
  height: 165px;
  border: 3px solid #aaa;
}
.part img {
  width: 165px;
}
.top-row {
  display: flex;
  justify-content: space-around;
}
.middle-row {
  display: flex;
  justify-content: center;
}
.bottom-row {
  display: flex;
  justify-content: space-around;
  border-top: none;
}
.head {
  border-bottom: none;
}
.left {
  border-right: none;
}
.right {
  border-left: none;
}
.left img {
  transform: rotate(-90deg);
}
.right img {
  transform: rotate(90deg);
}
.bottom {
  border-top: none;
}
.prev-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 171px;
}
.next-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 171px;
}
.center .prev-selector,
.center .next-selector {
  opacity: 0.8;
}
.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.right .prev-selector {
  top: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  right: -3px;
}
.robot-name {
  position: absolute;
  top: -25px;
  text-align: center;
  width: 100%;
}
</style>