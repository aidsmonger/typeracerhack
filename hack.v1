var charsPerIteration = 5;
var maxPressesPerSecond = 32;
var charsBeforeBackoff = 20;
var backoffDelayPerChar = 50;

var textElems = [].slice.call($("[unselectable='on']").parentNode.children);
var content = textElems.map(function (e) { return e.innerHTML; }).join('');
var input = $('.txtInput');
var startTime = void 0;
var keyPresses = 0;

setTimeout(function () {
    startTime = Date.now();
    write(content);
}, 1000);

function write(text, index) {
    if (index === void 0) index = 0;
    if (index >= text.length) return;

    input.focus();
    input.select();
    for (var i = 0; i < charsPerIteration && i < text.length; i++) {
        input.value += text[index + i];
        keyPresses++;
    }

    setTimeout(function () {
        write(text, index + charsPerIteration);
    }, delay());

    function delay() {
        var pressesPerSecond = 1000 * keyPresses / (Date.now() - startTime);

        // pps = wpm*5.1/60, where 5.1 is avg word length
        console.log("wpm: " + (pressesPerSecond * 60 / 5.1));

        if (keyPresses > charsBeforeBackoff
            && pressesPerSecond > maxPressesPerSecond) {
            return backoffDelayPerChar * charsPerIteration;
        }

        return 0;
    }
}
