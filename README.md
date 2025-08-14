<div [ngClass]="fileUploadButtonStyle" 
     (dragover)="onDragOver($event)" 
     (dragleave)="onDragLeave($event)" 
     (drop)="onDrop($event)"  
     [hidden]="!showUploadOpt">

  <div class="inner-dropZone">  
    <h3 class="txt-black">Drag files here</h3>  
    <p>Or, if you prefer ..</p>  
    <input type="file" 
           #uploader 
           class="btn-upload change-btn top-auto" 
           id="fileupload"
           (change)="fileSelection($event)" 
           multiple> <!-- Allow multiple file selection -->

    <button *ngIf="showFileUploader" 
            class="btn btn-primary btn-md" 
            (click)="uploader.click()">
      <span>Select files from your computer</span>
    </button>  

    <!-- Display file names when selected -->
    <div class="file-list" *ngIf="selectedFiles && selectedFiles.length > 0">
      <div *ngFor="let file of selectedFiles">
        {{ file.name }}
      </div>
    </div>

    <div class="changeBtn" *ngIf="!showFileUploader">  
      <div class="pull-left contain btn btn-primary pr24 p124 pte pba mt4 mr12">
        <span>Change</span> 
        <input type="file" 
               id="fileupload" 
               class="btn-upload change-btn" 
               (change)="fileSelection($event)" 
               multiple> <!-- Allow multiple here too -->
      </div>  

      <div class="pull-left mt4">  
        <div class="type-h5a txt-black">
          <span class="doc-name">{{ documentFile?.name }}</span>
        </div>  
      </div>  

      <div class="type-h5a light doc-desc" *ngIf="documentFileStage">  
        <span class="doc-type">{{ documentFileStage.fileExtension }}</span>
        <span class="doc-size">{{ documentFileStage.fileSize }}</span>
        <span class="doc-date">{{ documentFileStage.fileDate }}</span>
      </div>  
    </div>  
  </div>  

  <div *ngIf="isFileSizeMoreThan4Mb">
    Exceeded the size of 4 MB with {{ (documentFile.size / 1048576) | number: '1.2-2' }} MB
  </div>  

  <div *ngIf="showOtherProperties" [ngClass]="fileUploadButtonStyle">  
    <div class="fileName-container">  
      <div *ngIf="isFileUploadingStarted || isFileVerificationStarted || isValidationFailed || isFileUploaded">  
        <b>Selected File:</b>
      </div>

      <div *ngIf="isFileUploadingStarted || isFileVerificationStarted || isValidationFailed || isFileUploaded">  
        {{ documentFile?.name }}
      </div>

      <div>{{ documentFile?.size }}</div>

      <div class="ml-60 mt12" *ngIf="isFileVerificationStarted || isFileUploadingStarted"  
           [hidden]="isValidationFailed || isFileUploaded">
        <span class="loading-bar">  
          <div class="loading-bar-rotator">  
            <div class="loading-bar-spinner"></div>  
            <div class="loading-bar-spinner"></div>  
          </div>  
        </span>  
        <span *ngIf="isFileVerificationStarted">Virus scan in progress...</span>
        <span *ngIf="isFileUploadingStarted">Uploading File...</span>
      </div>  

      <div class="mt12" *ngIf="isFileUploaded">  
        <span class="material-icons success-icon">done</span>
        <span>Your file was successfully uploaded.</span>
      </div>
    </div>  
  </div>  
</div>
