namespace mask

import std.io.*
import java.io.*
import java.util.ArrayDeque

fun main(args : Array<String>) {
    val input = BufferedReader(InputStreamReader(System.`in`))

    val luhny = Luhny()
    forEachCharOf (input) {
        luhny.process(it)
    }
    luhny.printAll()
}

fun forEachCharOf(reader : Reader, body : fun(Char) : Unit) {
    while (true) {
        var i = reader.read();
        if (i == -1) break
        body(i.chr)
    }
}

class Luhny() {
    private val buffer = ArrayDeque<Char>()
    private val digits = ArrayDeque<Int>(16)

    private var toBeMasked = 0

    fun process(it : Char) {
        buffer.addLast(it)
        when (it) {
            .isDigit() => digits.addLast(it.toDigit())
            ' ', '-'   => {}
            else       => printAll()
        }
        if (digits.size() > 16) {
            printUntil { it.isDigit() }
            digits.removeFirst()
        }
        check()
    }

    private fun check() {
        val size = digits.size()
        if (size < 14) return

        var sum = 0
        var i = 0
        for (d in digits) {
            sum += if (i % 2 == size % 2) double(d) else d
            i++
        }

        if (sum % 10 == 0)
            toBeMasked = size
    }

    private fun double(d : Int) = d * 2 / 10 + d * 2 % 10

    fun printAll() {
        printUntil { false }
        digits.clear()
    }

    private fun printUntil(f : fun(Char) : Boolean) {
        while (!buffer.isEmpty()) {
            val c = buffer.removeFirst()
            printChar(c)
            if (f(c)) return
        }
    }

    private fun printChar(c : Char) {
        if (c.isDigit() && toBeMasked > 0) {
            print('X')
            toBeMasked--
        } else {
            print(c)
        }
    }
}

fun Char.isDigit() = Character.isDigit(this)
fun Char.toDigit() = this.int - '0'.int