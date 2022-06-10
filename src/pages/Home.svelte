<script lang="ts">

    // gloabl imports

    import Fa from 'svelte-fa/src/fa.svelte'
    import { faPlus } from '@fortawesome/free-solid-svg-icons'

    // type imports

    import type { NoteType } from '@/types/app'

    // component imports

    import Note from '@/components/Note.svelte'
    import EditNoteModal from '@/components/EditNoteModal.svelte'
    import DeleteNoteModal from '@/components/DeleteNoteModal.svelte'

    // variables declarations

    let notesJSONString: string = localStorage.getItem('notes')
    let notes: Array<NoteType> = []

    // notes initialisation

    if (notesJSONString) {
        try {
            notes = JSON.parse(notesJSONString) as NoteType[]
        } catch (error) {
            console.log(error)
        }
    } else {
        notes = [
            {
                id: 1,
                title: 'Some Note',
                content: 'this note is about this and that',
                date: '20210806123021',
                isFavorite: false,
                tags: ['test', 'text']
            },
            {
                id: 2,
                title: 'Another Note',
                content: 'this note is about this and that',
                date: '20210806133021',
                isFavorite: false,
                tags: ['test', 'text', 'extra']
            },
            {
                id: 3,
                title: 'Lorem ipsum',
                content: 'this note is about this and that',
                date: '20210806133021',
                isFavorite: true,
                tags: ['Lorem', 'ipsum']
            },
        ]
    }

    // Edit Modal Methods

    // for editing

    let noteToEdit: NoteType | Record<string, unknown> | undefined
    let showEditModal = false

    /**
    * Display the Note details modal
    *
    * @param {NoteType} note
    */

    const openEditNote = (note?: NoteType) => {
        noteToEdit = {}
        if (note) {
            noteToEdit = note
        }
        showEditModal = true
    }

    /**
    * Close the Note details modal
    *
    */

    const closeEditModal = () => {
        noteToEdit = {}
        showEditModal = false
    }

    // Delete Modal Methods

    // For Deleting

    let noteToDelete: NoteType | Record<string, unknown> | undefined
    let showDeleteModal = false

    /**
    * Display the Note details modal
    *
    * @param {NoteType} note
    */

    const openDeleteNote = (event: CustomEvent) => {
        const deleteNoteIndex = event.detail as number
        const noteIndex = notes.findIndex(item => item.id === deleteNoteIndex)
        if (noteIndex !== -1) {
            noteToDelete = notes[noteIndex]
            showDeleteModal = true
        }
    }

    /**
    * Close the Note details modal
    *
    */

    const closeDeleteModal = () => {
        noteToDelete = {}
        showDeleteModal = false
    }

    //  Note Related Methods
    /**
    * Save notes in the local storage
    */

    const saveNotesToStorage = () => {
        notes = notes
        localStorage.setItem('notes', JSON.stringify(notes))
    }

    /**
    * Toggle the favorite flag of a given post
    * and save the changes to local storage
    *
    * @param {CustomEvent} event
    * @param {Number} event.detail
    */

    const toggleFavorite = (event: CustomEvent) => {
        const noteId: number = (event.detail as number)
        const note = notes.find(item => item.id === noteId)
        if (note) {
            note.isFavorite = !note.isFavorite
            saveNotesToStorage()
        }
    }

    /**
    * Update the eixting note or add the new note
    *
    * @param {CustomEvent} event
    * @NoteType {Number} event.detail
    */

    const saveNote = (event: CustomEvent) => {
        closeEditModal()
        const note = event.detail as NoteType
        const noteIndex = notes.findIndex(item => item.id === note.id)

        if (noteIndex !== -1) {
            notes[noteIndex] = note
        } else {
            notes.push(note)
        }
        saveNotesToStorage()
    }


    /**
    *
    * @param {CustomEvent} event
    * @param {Number} event.detail
    */

    const deleteNote  = (event: CustomEvent) => {
        closeDeleteModal()
        closeEditModal()
        const deleteNoteIndex = event.detail as number
        const noteIndex = notes.findIndex(item => item.id === deleteNoteIndex)

        if (noteIndex !== -1) {
            notes.splice(noteIndex, 1)
        }
        console.log(notes)
        saveNotesToStorage()
    }
</script>

<div class="note-card-container">
    <div class="note-card-add" on:click="{() => { openEditNote() }}">
        <Fa icon={faPlus} color="#afaeae" size="3x" />
    </div>

    {#each notes as note (note.id)}
        <Note
            {...note}
            on:click="{() => {openEditNote(note)}}"
            on:toggleFavorite="{toggleFavorite}"
        />
    {/each}
</div>

{#if showEditModal}
    <EditNoteModal
        {...noteToEdit}
        on:save="{saveNote}"
        on:delete="{openDeleteNote}"
        on:close="{closeEditModal}"
    />
{/if}


{#if showDeleteModal}
    <DeleteNoteModal
        {...noteToDelete}
        on:delete="{deleteNote}"
        on:close="{closeDeleteModal}"
    />
{/if}


<style lang="scss">
    .note-card {
        &-add {
            background-color: #d6d4d4;
            display: flex;
            justify-content: center;
            align-items: center;
            box-shadow: none;
            border: 4px dashed #a29f9f;
            width: 144px;
            height: 189px;
            color: #a29f9f;
            margin-right: 15px;
            padding: 15px;
            border-radius: 10px;
            &:hover {
                background-color: #c5c5c5;
            }
        }

        &-container {
            display: flex;
        }
    }
</style>
